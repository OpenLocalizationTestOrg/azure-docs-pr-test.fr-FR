---
title: "Activation de l’authentification unique entre applications sur iOS à l’aide de la bibliothèque ADAL | Microsoft Docs"
description: "En savoir plus sur l’utilisation des fonctionnalités de votre Kit de développement logiciel (SDK) ADAL pour activer l’authentification unique sur l’ensemble de vos applications. "
services: active-directory
documentationcenter: 
author: brandwe
manager: mbaldwin
editor: 
ms.assetid: d042d6da-7503-4e20-bb55-06917de01fcd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: ios
ms.devlang: objective-c
ms.topic: article
ms.date: 04/07/2017
ms.author: brandwe
ms.custom: aaddev
ms.openlocfilehash: 73b8ed7e6a153a0790f7eae9bd51bb2e554ae72e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-enable-cross-app-sso-on-ios-using-adal"></a><span data-ttu-id="3f78e-103">Activation d’une authentification unique entre applications sur iOS à l’aide de la bibliothèque ADAL</span><span class="sxs-lookup"><span data-stu-id="3f78e-103">How to enable cross-app SSO on iOS using ADAL</span></span>
<span data-ttu-id="3f78e-104">Les clients s’attendent désormais à profiter d’une authentification unique, nécessitant des utilisateurs une seule et unique saisie des informations d’identification, qui restent automatiquement actives sur l’ensemble des applications.</span><span class="sxs-lookup"><span data-stu-id="3f78e-104">Providing Single Sign-On (SSO) so that users only need to enter their credentials once and have those credentials automatically work across applications is now expected by customers.</span></span> <span data-ttu-id="3f78e-105">La difficulté à saisir le nom d’utilisateur et le mot de passe sur des petits formats d’écrans, à laquelle s’ajoute souvent un facteur supplémentaire (2FA) tel qu’un appel ou un code par SMS, mécontente rapidement les utilisateurs contraints d’effectuer plusieurs fois l’opération pour votre produit.</span><span class="sxs-lookup"><span data-stu-id="3f78e-105">The difficulty in entering their username and password on a small screen, often times combined with an additional factor (2FA) like a phone call or a texted code, results in quick dissatisfaction if a user has to do this more than one time for your product.</span></span>

<span data-ttu-id="3f78e-106">En outre, si vous mettez en œuvre une plateforme d’identité que d’autres applications peuvent utiliser, telle que les comptes Microsoft ou un compte professionnel d’Office365, les clients s’attendent à ce que ces informations d’identification soient disponibles sur l’ensemble de leurs applications, quel que soit le fournisseur.</span><span class="sxs-lookup"><span data-stu-id="3f78e-106">In addition, if you apply an identity platform that other applications may use such as Microsoft Accounts or a work account from Office365, customers expect that those credentials to be available to use across all their applications no matter the vendor.</span></span>

<span data-ttu-id="3f78e-107">La plateforme Microsoft Identity, combinée à nos Kits de développement logiciel (SDK) Microsoft Identity, vous soulage de ces tâches complexes et vous permet d’offrir à vos utilisateurs l’authentification unique au sein de votre propre suite d’applications, ou, comme avec nos applications de répartiteur et Authenticator, sur l’intégralité de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="3f78e-107">The Microsoft Identity platform, along with our Microsoft Identity SDKs, does all this hard work for you and gives you the ability to delight your customers with SSO either within your own suite of applications or, as with our broker capability and Authenticator applications, across the entire device.</span></span>

<span data-ttu-id="3f78e-108">Cette procédure pas à pas vous décrit la configuration de notre Kit de développement logiciel (SDK) au sein de votre application afin d’offrir cet avantage à vos clients.</span><span class="sxs-lookup"><span data-stu-id="3f78e-108">This walkthrough will tell you how to configure our SDK within your application to provide this benefit to your customers.</span></span>

<span data-ttu-id="3f78e-109">Cette procédure pas à pas s’applique aux éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="3f78e-109">This walkthrough applies to:</span></span>

* <span data-ttu-id="3f78e-110">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3f78e-110">Azure Active Directory</span></span>
* <span data-ttu-id="3f78e-111">Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="3f78e-111">Azure Active Directory B2C</span></span>
* <span data-ttu-id="3f78e-112">Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="3f78e-112">Azure Active Directory B2B</span></span>
* <span data-ttu-id="3f78e-113">Accès conditionnel Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3f78e-113">Azure Active Directory Conditional Access</span></span>

<span data-ttu-id="3f78e-114">Le document ci-dessus prend pour acquis que vous savez comment [mettre en service des applications dans le portail hérité dédié Azure Active Directory](active-directory-how-to-integrate.md) et que vous avez intégré votre application avec le [Kit de développement logiciel (SDK) Microsoft Identity iOS](https://github.com/AzureAD/azure-activedirectory-library-for-objc).</span><span class="sxs-lookup"><span data-stu-id="3f78e-114">The document preceding assumes you know how to [provision applications in the legacy portal for Azure Active Directory](active-directory-how-to-integrate.md) and integrated your application with the [Microsoft Identity iOS SDK](https://github.com/AzureAD/azure-activedirectory-library-for-objc).</span></span>

## <a name="sso-concepts-in-the-microsoft-identity-platform"></a><span data-ttu-id="3f78e-115">Concepts de l’authentification unique dans la plateforme Microsoft Identity</span><span class="sxs-lookup"><span data-stu-id="3f78e-115">SSO Concepts in the Microsoft Identity Platform</span></span>
### <a name="microsoft-identity-brokers"></a><span data-ttu-id="3f78e-116">Répartiteurs Microsoft Identity</span><span class="sxs-lookup"><span data-stu-id="3f78e-116">Microsoft Identity Brokers</span></span>
<span data-ttu-id="3f78e-117">Sur l’ensemble des plateformes mobiles, Microsoft fournit des applications qui prennent en charge le portage des informations d’identification entre les applications de différents fournisseurs, ainsi que des fonctionnalités spéciales avancées nécessitant un emplacement unique sécurisé de validation des informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="3f78e-117">Microsoft provides applications for every mobile platform that allow for the bridging of credentials across applications from different vendors and allows for special enhanced features that require a single secure place from where to validate credentials.</span></span> <span data-ttu-id="3f78e-118">Nous appelons ces applications **répartiteurs**.</span><span class="sxs-lookup"><span data-stu-id="3f78e-118">We call these **brokers**.</span></span> <span data-ttu-id="3f78e-119">Sur iOS et Android, ces répartiteurs sont offerts via des applications téléchargeables que les clients installent indépendamment ou sont transmis sur l’appareil par une entreprise qui gère certains ou la totalité des appareils des employés.</span><span class="sxs-lookup"><span data-stu-id="3f78e-119">On iOS and Android these brokers are provided through downloadable applications that customers either install independently or can be pushed to the device by a company who manages some or all of the device for their employee.</span></span> <span data-ttu-id="3f78e-120">Ces répartiteurs gèrent la sécurité d’une partie des applications ou de l’intégralité de l’appareil, en fonction des besoins des administrateurs informatiques.</span><span class="sxs-lookup"><span data-stu-id="3f78e-120">These brokers support managing security just for some applications or the entire device based on what IT Administrators desire.</span></span> <span data-ttu-id="3f78e-121">Dans Windows, cette fonctionnalité est fournie par un sélecteur de compte intégré au système d’exploitation, désigné techniquement sous l’appellation « Répartiteur d’authentification web ».</span><span class="sxs-lookup"><span data-stu-id="3f78e-121">In Windows, this functionality is provided by an account chooser built in to the operating system, known technically as the Web Authentication Broker.</span></span>

<span data-ttu-id="3f78e-122">Pour plus d’informations sur l’utilisation de ces répartiteurs et sur la manière dont vos utilisateurs peuvent les afficher dans leurs flux de connexion associés à la plateforme Microsoft Identity, consultez les références suivantes.</span><span class="sxs-lookup"><span data-stu-id="3f78e-122">For more information on how we use these brokers and how your customers might see them in their login flow for the Microsoft Identity platform read on.</span></span>

### <a name="patterns-for-logging-in-on-mobile-devices"></a><span data-ttu-id="3f78e-123">Modèles de connexion sur les appareils mobiles</span><span class="sxs-lookup"><span data-stu-id="3f78e-123">Patterns for logging in on mobile devices</span></span>
<span data-ttu-id="3f78e-124">L’accès aux informations d’identification sur les appareils respecte deux modèles de base pour la plateforme Microsoft Identity :</span><span class="sxs-lookup"><span data-stu-id="3f78e-124">Access to credentials on devices follow two basic patterns for the Microsoft Identity platform:</span></span>

* <span data-ttu-id="3f78e-125">Connexions assistées sans répartiteur</span><span class="sxs-lookup"><span data-stu-id="3f78e-125">Non-broker assisted logins</span></span>
* <span data-ttu-id="3f78e-126">Connexions assistées avec répartiteur</span><span class="sxs-lookup"><span data-stu-id="3f78e-126">Broker assisted logins</span></span>

#### <a name="non-broker-assisted-logins"></a><span data-ttu-id="3f78e-127">Connexions assistées sans répartiteur</span><span class="sxs-lookup"><span data-stu-id="3f78e-127">Non-broker assisted logins</span></span>
<span data-ttu-id="3f78e-128">Les connexions assistées sans répartiteur correspondent à des expériences de connexion intervenant en ligne avec l’application et utilisant le stockage local sur l’appareil pour cette application.</span><span class="sxs-lookup"><span data-stu-id="3f78e-128">Non-broker assisted logins are login experiences that happen inline with the application and use the local storage on the device for that application.</span></span> <span data-ttu-id="3f78e-129">Ce stockage peut être partagé entre les applications, mais les informations d’identification sont étroitement liées à l’application ou à la suite d’applications qui les utilisent.</span><span class="sxs-lookup"><span data-stu-id="3f78e-129">This storage may be shared across applications but the credentials are tightly bound to the app or suite of apps using that credential.</span></span> <span data-ttu-id="3f78e-130">Vous avez probablement eu cette expérience sur de nombreuses applications mobiles, lorsque vous devez saisir un nom d’utilisateur et un mot de passe.</span><span class="sxs-lookup"><span data-stu-id="3f78e-130">You've most likely experienced this in many mobile applications when you enter a username and password within the application itself.</span></span>

<span data-ttu-id="3f78e-131">Ces connexions présentent les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="3f78e-131">These logins have the following benefits:</span></span>

* <span data-ttu-id="3f78e-132">L’expérience utilisateur existe intégralement au sein de l’application.</span><span class="sxs-lookup"><span data-stu-id="3f78e-132">User experience exists entirely within the application.</span></span>
* <span data-ttu-id="3f78e-133">Les informations d’identification peuvent être partagées entre les applications qui sont signées par le même certificat, ce qui constitue une expérience de connexion unique à votre suite d’applications.</span><span class="sxs-lookup"><span data-stu-id="3f78e-133">Credentials can be shared across applications that are signed by the same certificate, providing a single sign-on experience to your suite of applications.</span></span>
* <span data-ttu-id="3f78e-134">Le contrôle de connexion est fourni à l’application avant et après la connexion.</span><span class="sxs-lookup"><span data-stu-id="3f78e-134">Control around the experience of logging in is provided to the application before and after sign-in.</span></span>

<span data-ttu-id="3f78e-135">Ces connexions présentent les inconvénients suivants :</span><span class="sxs-lookup"><span data-stu-id="3f78e-135">These logins have the following drawbacks:</span></span>

* <span data-ttu-id="3f78e-136">L’utilisateur ne peut pas profiter de l’authentification unique sur l’ensemble des applications utilisant Microsoft Identity, uniquement sur celles que votre application a configuré.</span><span class="sxs-lookup"><span data-stu-id="3f78e-136">User cannot experience single-sign on across all apps that use a Microsoft Identity, only across those Microsoft Identities that your application has configured.</span></span>
* <span data-ttu-id="3f78e-137">Votre application ne peut pas être utilisée avec des fonctionnalités commerciales plus avancées, comme l’accès conditionnel ; elle ne peut pas non plus utiliser la suite de produits Intune.</span><span class="sxs-lookup"><span data-stu-id="3f78e-137">Your application cannot be used with more advanced business features such as Conditional Access or use the InTune suite of products.</span></span>
* <span data-ttu-id="3f78e-138">Votre application ne peut pas prendre en charge l’authentification par certificat des utilisateurs professionnels.</span><span class="sxs-lookup"><span data-stu-id="3f78e-138">Your application can't support certificate-based authentication for business users.</span></span>

<span data-ttu-id="3f78e-139">Voici une représentation de la manière dont les Kits de développement logiciel (SDK) Microsoft Identity fonctionnent avec le stockage partagé de vos applications, pour l’activation de l’authentification unique :</span><span class="sxs-lookup"><span data-stu-id="3f78e-139">Here is a representation of how the Microsoft Identity SDKs work with the shared storage of your applications to enable SSO:</span></span>

```
+------------+ +------------+  +-------------+
|            | |            |  |             |
|   App 1    | |   App 2    |  |   App 3     |
|            | |            |  |             |
|            | |            |  |             |
+------------+ +------------+  +-------------+
| ADAL SDK  |  |  ADAL SDK  |  |  ADAK SDK   |
+------------+-+------------+--+-------------+
|                                            |
|            App Shared Storage              |
+--------------------------------------------+
```

#### <a name="broker-assisted-logins"></a><span data-ttu-id="3f78e-140">Connexions assistées avec répartiteur</span><span class="sxs-lookup"><span data-stu-id="3f78e-140">Broker assisted logins</span></span>
<span data-ttu-id="3f78e-141">Les connexions assistées avec répartiteur sont des expériences de connexion se produisant au sein de l’application de répartiteur, qui utilisent le stockage et la sécurité de ce composant pour partager l’ensemble des applications sur l’appareil qui applique la plateforme Microsoft Identity.</span><span class="sxs-lookup"><span data-stu-id="3f78e-141">Broker-assisted logins are login experiences that occur within the broker application and use the storage and security of the broker to share credentials across all applications on the device that apply the Microsoft Identity platform.</span></span> <span data-ttu-id="3f78e-142">Vos applications s’appuient sur le répartiteur pour connecter les utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="3f78e-142">This means that your applications rely on the broker to sign users in.</span></span> <span data-ttu-id="3f78e-143">Sur iOS et Android, ces répartiteurs sont fournis via des applications téléchargeables que les clients installent indépendamment ou sont transmis sur l’appareil par une entreprise qui gère les appareils des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="3f78e-143">On iOS and Android these brokers are provided through downloadable applications that customers either install independently or can be pushed to the device by a company who manages the device for their user.</span></span> <span data-ttu-id="3f78e-144">Comme exemple de ce type d’application, citons Microsoft Authenticator sur iOS.</span><span class="sxs-lookup"><span data-stu-id="3f78e-144">An example of this type of application is the Microsoft Authenticator application on iOS.</span></span> <span data-ttu-id="3f78e-145">Dans Windows, cette fonctionnalité est fournie par un sélecteur de compte intégré au système d’exploitation, désigné techniquement sous l’appellation « Répartiteur d’authentification web ».</span><span class="sxs-lookup"><span data-stu-id="3f78e-145">In Windows this functionality is provided by an account chooser built in to the operating system, known technically as the Web Authentication Broker.</span></span>
<span data-ttu-id="3f78e-146">L’expérience, qui varie en fonction des plateformes, peut parfois perturber les utilisateurs en cas de gestion inappropriée.</span><span class="sxs-lookup"><span data-stu-id="3f78e-146">The experience varies by platform and can sometimes be disruptive to users if not managed correctly.</span></span> <span data-ttu-id="3f78e-147">Vous connaissez probablement davantage ce modèle si vous avez installé l’application Facebook et que vous utilisez Facebook Connect depuis une autre application.</span><span class="sxs-lookup"><span data-stu-id="3f78e-147">You're probably most familiar with this pattern if you have the Facebook application installed and use Facebook Connect from another application.</span></span> <span data-ttu-id="3f78e-148">La plateforme Microsoft Identity utilise le même modèle.</span><span class="sxs-lookup"><span data-stu-id="3f78e-148">The Microsoft Identity platform uses the same pattern.</span></span>

<span data-ttu-id="3f78e-149">Sur iOS, une animation de transition s’affiche. Votre application est transmise à l’arrière-plan, tandis que les applications Microsoft Authenticator sont mises en avant-plan, ce qui permet à l’utilisateur de choisir son compte de connexion.</span><span class="sxs-lookup"><span data-stu-id="3f78e-149">For iOS this leads to a "transition" animation where your application is sent to the background while the Microsoft Authenticator applications comes to the foreground for the user to select which account they would like to sign in with.</span></span>  

<span data-ttu-id="3f78e-150">Sur Android et Windows, le sélecteur de compte s’affiche dans la partie supérieure de votre application ; l’utilisateur est ainsi moins perturbé.</span><span class="sxs-lookup"><span data-stu-id="3f78e-150">For Android and Windows the account chooser is displayed on top of your application which is less disruptive to the user.</span></span>

#### <a name="how-the-broker-gets-invoked"></a><span data-ttu-id="3f78e-151">Appel du répartiteur</span><span class="sxs-lookup"><span data-stu-id="3f78e-151">How the broker gets invoked</span></span>
<span data-ttu-id="3f78e-152">Si un répartiteur compatible, tel que l’application Microsoft Authenticator, est installé sur l’appareil, les Kits de développement logiciel (SDK) Microsoft Identity effectuent automatiquement pour vous l’opération d’appel du répartiteur lorsqu’un utilisateur souhaite se connecter à l’aide d’un compte de la plateforme Microsoft Identity.</span><span class="sxs-lookup"><span data-stu-id="3f78e-152">If a compatible broker is installed on the device, like the Microsoft Authenticator application, the Microsoft Identity SDKs will automatically do the work of invoking the broker for you when a user indicates they wish to log in using any account from the Microsoft Identity platform.</span></span> <span data-ttu-id="3f78e-153">Il peut s’agir d’un compte personnel Microsoft, d’un compte professionnel ou scolaire, ou d’un compte que vous fournissez et hébergez dans Microsoft Azure à l’aide de nos produits B2C et B2B.</span><span class="sxs-lookup"><span data-stu-id="3f78e-153">This account could be a personal Microsoft Account, a work or school account, or an account that you provide and host in Azure using our B2C and B2B products.</span></span> 

 #### <a name="how-we-ensure-the-application-is-valid"></a><span data-ttu-id="3f78e-154">Comment s’assurer que l’application est valide</span><span class="sxs-lookup"><span data-stu-id="3f78e-154">How we ensure the application is valid</span></span>
 
 <span data-ttu-id="3f78e-155">Pour sécuriser les connexions assistées avec répartiteur, il est essentiel de s’assurer de l’identité de l’application appelant le répartiteur.</span><span class="sxs-lookup"><span data-stu-id="3f78e-155">The need to ensure the identity of an application call the broker is crucial to the security we provide in broker assisted logins.</span></span> <span data-ttu-id="3f78e-156">iOS et Android ne fournissent pas d’identificateurs uniques valides uniquement pour une application donnée. Ainsi, des applications malveillantes peuvent « usurper » l’identité d’une application légitime en utilisant son identificateur et recevoir les jetons destinés à l’application légitime.</span><span class="sxs-lookup"><span data-stu-id="3f78e-156">Neither iOS nor Android enforces unique identifiers that are valid only for a given application, so malicious applications may "spoof" a legitimate application's identifier and receive the tokens meant for the legitimate application.</span></span> <span data-ttu-id="3f78e-157">Pour être sûrs de toujours communiquer avec la bonne application au moment de l’exécution, nous demandons aux développeurs de fournir un URI de redirection (redirectURI) personnalisé lorsqu’ils inscrivent leur application auprès de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="3f78e-157">To ensure we are always communicating with the right application at runtime, we ask the developer to provide a custom redirectURI when registering their application with Microsoft.</span></span> <span data-ttu-id="3f78e-158">**Nous expliquons ci-dessous comment les développeurs doivent créer cet URI de redirection.**</span><span class="sxs-lookup"><span data-stu-id="3f78e-158">**How developers should craft this redirect URI is discussed in detail below.**</span></span> <span data-ttu-id="3f78e-159">Cet URI de redirection personnalisé contient l’ID d’offre groupée de l’application et est garanti comme étant propre à l’application par l’App Store.</span><span class="sxs-lookup"><span data-stu-id="3f78e-159">This custom redirectURI contains the Bundle ID of the application and is ensured to be unique to the application by the Apple App Store.</span></span> <span data-ttu-id="3f78e-160">Lorsqu’une application appelle le répartiteur, celui-ci demande au système d’exploitation iOS de lui fournir l’ID d’offre groupée qui a appelé le répartiteur.</span><span class="sxs-lookup"><span data-stu-id="3f78e-160">When an application calls the broker, the broker asks the iOS operating system to provide it with the Bundle ID that called the broker.</span></span> <span data-ttu-id="3f78e-161">Le répartiteur fournit cet l’ID d’offre groupée à Microsoft dans le cadre de l’appel à notre système d’identité.</span><span class="sxs-lookup"><span data-stu-id="3f78e-161">The broker provides this Bundle ID to Microsoft in the call to our identity system.</span></span> <span data-ttu-id="3f78e-162">Si l’ID d’offre groupée de l’application ne correspond pas à l’ID d’offre groupée fourni par le développeur au moment de l’inscription, nous refusons l’accès aux jetons de la ressource dont l’application a fait la demande.</span><span class="sxs-lookup"><span data-stu-id="3f78e-162">If the Bundle ID of the application does not match the Bundle ID provided to us by the developer during registration, we will deny access to the tokens for the resource the application is requesting.</span></span> <span data-ttu-id="3f78e-163">Cette vérification permet de s’assurer que seule l’application inscrite par le développeur reçoit les jetons.</span><span class="sxs-lookup"><span data-stu-id="3f78e-163">This check ensures that only the application registered by the developer receives tokens.</span></span>

<span data-ttu-id="3f78e-164">**Le développeur détermine si le kit de développement logiciel (SDK) appelle le répartiteur ou utilise un flux assisté sans répartiteur.**</span><span class="sxs-lookup"><span data-stu-id="3f78e-164">**The developer has the choice of if the Microsoft Identity SDK calls the broker or uses the non-broker assisted flow.**</span></span> <span data-ttu-id="3f78e-165">Toutefois, si le développeur choisit de ne pas avoir recours au flux assisté avec répartiteur, il ne peut pas utiliser les informations d’identification d’authentification unique déjà saisies par l’utilisateur sur l’appareil et il empêche toute utilisation de l’application avec des fonctions commerciales fournies par Microsoft à ses clients, comme l’accès conditionnel, les fonctionnalités de gestion Intune et l’authentification par certificat.</span><span class="sxs-lookup"><span data-stu-id="3f78e-165">However if the developer chooses not to use the broker-assisted flow they lose the benefit of using SSO credentials that the user may have already added on the device and prevents their application from being used with business features Microsoft provides its customers such as Conditional Access, Intune Management capabilities, and certificate-based authentication.</span></span>

<span data-ttu-id="3f78e-166">Ces connexions présentent les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="3f78e-166">These logins have the following benefits:</span></span>

* <span data-ttu-id="3f78e-167">L’utilisateur profite de l’authentification unique sur l’ensemble de ses applications, quel que soit le fournisseur.</span><span class="sxs-lookup"><span data-stu-id="3f78e-167">User experiences SSO across all their applications no matter the vendor.</span></span>
* <span data-ttu-id="3f78e-168">Votre application peut utiliser des fonctionnalités commerciales plus avancées, comme l’accès conditionnel, ou la suite de produits Intune.</span><span class="sxs-lookup"><span data-stu-id="3f78e-168">Your application can use more advanced business features such as Conditional Access or use the InTune suite of products.</span></span>
* <span data-ttu-id="3f78e-169">Votre application peut prendre en charge l’authentification par certificat des utilisateurs professionnels.</span><span class="sxs-lookup"><span data-stu-id="3f78e-169">Your application can support certificate-based authentication for business users.</span></span>
* <span data-ttu-id="3f78e-170">L’expérience de connexion est bien plus sécurisée, dans la mesure où les identités de l’application et de l’utilisateur sont vérifiées par l’application du répartiteur à l’aide d’algorithmes de sécurité et d’un chiffrement supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="3f78e-170">Much more secure sign-in experience as the identity of the application and the user are verified by the broker application with additional security algorithms and encryption.</span></span>

<span data-ttu-id="3f78e-171">Ces connexions présentent les inconvénients suivants :</span><span class="sxs-lookup"><span data-stu-id="3f78e-171">These logins have the following drawbacks:</span></span>

* <span data-ttu-id="3f78e-172">Dans iOS, l’utilisateur est déplacé à l’extérieur de l’expérience applicative pendant la sélection des informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="3f78e-172">In iOS the user is transitioned out of your application's experience while credentials are chosen.</span></span>
* <span data-ttu-id="3f78e-173">Perte de la capacité de gérer l’expérience de connexion des clients au sein de l’application.</span><span class="sxs-lookup"><span data-stu-id="3f78e-173">Loss of the ability to manage the login experience for your customers within your application.</span></span>

<span data-ttu-id="3f78e-174">Voici une représentation de la manière dont les Kits de développement logiciel (SDK) Microsoft Identity fonctionnent avec les applications de répartiteur pour prendre en charge l’authentification unique :</span><span class="sxs-lookup"><span data-stu-id="3f78e-174">Here is a representation of how the Microsoft Identity SDKs work with the broker applications to enable SSO:</span></span>

```
+------------+ +------------+   +-------------+
|            | |            |   |             |
|   App 1    | |   App 2    |   |   Someone   |
|            | |            |   |    Else's   |
|            | |            |   |     App     |
+------------+ +------------+   +-------------+
| Azure SDK  | | Azure SDK  |   | Azure SDK   |
+-----+------+-+-----+------+-  +-------+-----+
      |              |                  |
      |       +------v------+           |
      |       |             |           |
      |       | Microsoft   |           |
      +-------> Broker      |^----------+
              | Application
              |             |
              +-------------+
              |             |
              |   Broker    |
              |   Storage   |
              |             |
              +-------------+
```

<span data-ttu-id="3f78e-175">En vous appuyant sur ces informations de base, vous devriez être en mesure de mieux comprendre et d’implémenter l’authentification unique au sein de votre application à l’aide de la plateforme et des Kits de développement logiciel (SDK) Microsoft Identity.</span><span class="sxs-lookup"><span data-stu-id="3f78e-175">Armed with this background information you should be able to better understand and implement SSO within your application using the Microsoft Identity platform and SDKs.</span></span>

## <a name="enabling-cross-app-sso-using-adal"></a><span data-ttu-id="3f78e-176">Activation de l’authentification unique entre applications à l’aide de la bibliothèque ADAL</span><span class="sxs-lookup"><span data-stu-id="3f78e-176">Enabling cross-app SSO using ADAL</span></span>
<span data-ttu-id="3f78e-177">Ici, nous utilisons le Kit de développement logiciel ADAL iOS pour effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="3f78e-177">Here we use the ADAL iOS SDK to:</span></span>

* <span data-ttu-id="3f78e-178">Activer l’authentification unique assistée sans répartiteur pour votre suite d’applications</span><span class="sxs-lookup"><span data-stu-id="3f78e-178">Turn on non-broker assisted SSO for your suite of apps</span></span>
* <span data-ttu-id="3f78e-179">Activer la prise en charge de l’authentification unique assistée avec répartiteur</span><span class="sxs-lookup"><span data-stu-id="3f78e-179">Turn on support for broker-assisted SSO</span></span>

### <a name="turning-on-sso-for-non-broker-assisted-sso"></a><span data-ttu-id="3f78e-180">Activation de l’authentification unique assistée sans répartiteur</span><span class="sxs-lookup"><span data-stu-id="3f78e-180">Turning on SSO for non-broker assisted SSO</span></span>
<span data-ttu-id="3f78e-181">Les Kits de développement logiciel (SDK) Microsoft Identity prennent en charge une grande partie de la complexité de l’authentification unique assistée sans répartiteur entre les applications.</span><span class="sxs-lookup"><span data-stu-id="3f78e-181">For non-broker assisted SSO across applications the Microsoft Identity SDKs manage much of the complexity of SSO for you.</span></span> <span data-ttu-id="3f78e-182">Cela inclut l’identification de l’utilisateur approprié dans le cache et la gestion d’une liste d’utilisateurs connectés dans laquelle effectuer votre recherche.</span><span class="sxs-lookup"><span data-stu-id="3f78e-182">This includes finding the right user in the cache and maintaining a list of logged in users for you to query.</span></span>

<span data-ttu-id="3f78e-183">Pour activer l’authentification unique sur l’ensemble des applications que vous possédez, vous devez effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="3f78e-183">To enable SSO across applications you own you need to do the following:</span></span>

1. <span data-ttu-id="3f78e-184">Vérifiez que l’ensemble de vos applications utilisent le même ID client ou ID d’application.</span><span class="sxs-lookup"><span data-stu-id="3f78e-184">Ensure all your applications user the same Client ID or Application ID.</span></span>
2. <span data-ttu-id="3f78e-185">Vérifiez que l’ensemble de vos applications partagent le même certificat de signature fourni par Apple, de manière à ce que vous puissiez partager les trousseaux.</span><span class="sxs-lookup"><span data-stu-id="3f78e-185">Ensure that all of your applications share the same signing certificate from Apple so that you can share keychains</span></span>
3. <span data-ttu-id="3f78e-186">Demandez la même éligibilité de trousseau pour l’ensemble de vos applications.</span><span class="sxs-lookup"><span data-stu-id="3f78e-186">Request the same keychain entitlement for each of your applications.</span></span>
4. <span data-ttu-id="3f78e-187">Indiquez aux Kits de développement logiciel Microsoft Identity le trousseau partagé que vous souhaitez utiliser.</span><span class="sxs-lookup"><span data-stu-id="3f78e-187">Tell the Microsoft Identity SDKs about the shared keychain you want us to use.</span></span>

#### <a name="using-the-same-client-id--application-id-for-all-the-applications-in-your-suite-of-apps"></a><span data-ttu-id="3f78e-188">Utilisation du même ID client/ID d’application pour l’ensemble des applications de votre suite d’applications</span><span class="sxs-lookup"><span data-stu-id="3f78e-188">Using the same Client ID / Application ID for all the applications in your suite of apps</span></span>
<span data-ttu-id="3f78e-189">Pour que votre plateforme Microsoft Identity puisse savoir que le partage des jetons est autorisé entre vos applications, elles doivent toutes partager le même ID client ou d’application.</span><span class="sxs-lookup"><span data-stu-id="3f78e-189">In order for the Microsoft Identity platform to know that it's allowed to share tokens across your applications, each of your applications will need to share the same Client ID or Application ID.</span></span> <span data-ttu-id="3f78e-190">Il s’agit de l’identificateur unique qui vous a été fourni lorsque vous avez inscrit votre première application dans le portail.</span><span class="sxs-lookup"><span data-stu-id="3f78e-190">This is the unique identifier that was provided to you when you registered your first application in the portal.</span></span>

<span data-ttu-id="3f78e-191">Vous vous demandez peut-être comment identifier différentes applications utilisant le même ID d’application sur un service Microsoft Identity.</span><span class="sxs-lookup"><span data-stu-id="3f78e-191">You may be wondering how you will identify different apps to the Microsoft Identity service if it uses the same Application ID.</span></span> <span data-ttu-id="3f78e-192">La réponse est à chercher du côté des **URI de redirection**.</span><span class="sxs-lookup"><span data-stu-id="3f78e-192">The answer is with the **Redirect URIs**.</span></span> <span data-ttu-id="3f78e-193">Chaque application peut posséder plusieurs URI de redirection inscrits sur le portail d’intégration.</span><span class="sxs-lookup"><span data-stu-id="3f78e-193">Each application can have multiple Redirect URIs registered in the onboarding portal.</span></span> <span data-ttu-id="3f78e-194">Chacune des applications de votre suite présente un URI de redirection propre.</span><span class="sxs-lookup"><span data-stu-id="3f78e-194">Each app in your suite will have a different redirect URI.</span></span> <span data-ttu-id="3f78e-195">Voici une représentation possible :</span><span class="sxs-lookup"><span data-stu-id="3f78e-195">An example of how this looks is below:</span></span>

<span data-ttu-id="3f78e-196">URI de redirection App1 : `x-msauth-mytestiosapp://com.myapp.mytestapp`</span><span class="sxs-lookup"><span data-stu-id="3f78e-196">App1 Redirect URI: `x-msauth-mytestiosapp://com.myapp.mytestapp`</span></span>

<span data-ttu-id="3f78e-197">URI de redirection App2 : `x-msauth-mytestiosapp://com.myapp.mytestapp2`</span><span class="sxs-lookup"><span data-stu-id="3f78e-197">App2 Redirect URI: `x-msauth-mytestiosapp://com.myapp.mytestapp2`</span></span>

<span data-ttu-id="3f78e-198">URI de redirection App3 : `x-msauth-mytestiosapp://com.myapp.mytestapp3`</span><span class="sxs-lookup"><span data-stu-id="3f78e-198">App3 Redirect URI: `x-msauth-mytestiosapp://com.myapp.mytestapp3`</span></span>

<span data-ttu-id="3f78e-199">....</span><span class="sxs-lookup"><span data-stu-id="3f78e-199">....</span></span>

<span data-ttu-id="3f78e-200">Ces éléments sont imbriqués sous le même ID client/ID d’application et recherchés en fonction de l’URI de redirection que vous nous transmettez dans votre configuration du Kit de développement logiciel (SDK).</span><span class="sxs-lookup"><span data-stu-id="3f78e-200">These are nested under the same client ID / application ID and looked up based on the redirect URI you return to us in your SDK configuration.</span></span>

```
+-------------------+
|                   |
|  Client ID        |
+---------+---------+
          |
          |           +-----------------------------------+
          |           |  App 1 Redirect URI               |
          +----------^+                                   |
          |           +-----------------------------------+
          |
          |           +-----------------------------------+
          +----------^+  App 2 Redirect URI               |
          |           |                                   |
          |           +-----------------------------------+
          |
          +----------^+-----------------------------------+
                      |  App 3 Redirect URI               |
                      |                                   |
                      +-----------------------------------+

```


<span data-ttu-id="3f78e-201">*Le format de ces URI de redirection est expliqué plus bas. Vous pouvez utiliser l’URI de redirection de votre choix, sauf si vous souhaitez prendre en charge le répartiteur. Le cas échéant, la configuration est similaire à ce qui précède*</span><span class="sxs-lookup"><span data-stu-id="3f78e-201">*Note that the format of these Redirect URIs are explained below. You may use any Redirect URI unless you wish to support the broker, in which case they must look something like the above*</span></span>

#### <a name="create-keychain-sharing-between-applications"></a><span data-ttu-id="3f78e-202">Créer le partage de trousseau entre les applications</span><span class="sxs-lookup"><span data-stu-id="3f78e-202">Create keychain sharing between applications</span></span>
<span data-ttu-id="3f78e-203">L’activation du partage de trousseau n’entre pas dans le périmètre de ce document. Le sujet est abordé par Apple, dans le document [Adding Capabilities](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html) (Ajout de fonctionnalités).</span><span class="sxs-lookup"><span data-stu-id="3f78e-203">Enabling keychain sharing is beyond the scope of this document and covered by Apple in their document [Adding Capabilities](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html).</span></span> <span data-ttu-id="3f78e-204">L’essentiel est que vous déterminiez le nom que vous souhaitez attribuer à votre trousseau et que vous ajoutiez cette fonctionnalité dans l’ensemble de vos applications.</span><span class="sxs-lookup"><span data-stu-id="3f78e-204">What is important is that you decide what you want your keychain to be called and add that capability across all your applications.</span></span>

<span data-ttu-id="3f78e-205">Une fois que vous disposez des droits appropriés, un fichier nommé `entitlements.plist` doit s’afficher dans votre répertoire de projet. Le cas échéant, il présente un contenu de ce type :</span><span class="sxs-lookup"><span data-stu-id="3f78e-205">When you do have entitlements set up correctly you should see a file in your project directory entitled `entitlements.plist` that contains something that looks like the following:</span></span>

```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
    <key>keychain-access-groups</key>
    <array>
        <string>$(AppIdentifierPrefix)com.myapp.mytestapp</string>
        <string>$(AppIdentifierPrefix)com.myapp.mycache</string>
    </array>
</dict>
</plist>
```

<span data-ttu-id="3f78e-206">Une fois que l’éligibilité au trousseau a été activée dans chacune de vos applications et que vous êtes prêt à utiliser l’authentification unique, communiquez votre trousseau au Kit de développement logiciel Microsoft Identity en utilisant le paramètre suivant dans votre `ADAuthenticationSettings`, à l’aide du paramètre ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="3f78e-206">Once you have the keychain entitlement enabled in each of your applications, and you are ready to use SSO, tell the Microsoft Identity SDK about your keychain by using the following setting in your `ADAuthenticationSettings` with the following setting:</span></span>

```
defaultKeychainSharingGroup=@"com.myapp.mycache";
```

> [!WARNING]
> <span data-ttu-id="3f78e-207">Lorsque vous partagez un trousseau entre vos applications, chaque application peut supprimer les utilisateurs, ou au pire l’ensemble des jetons de votre application.</span><span class="sxs-lookup"><span data-stu-id="3f78e-207">When you share a keychain across your applications any application can delete users or worse delete all the tokens across your application.</span></span> <span data-ttu-id="3f78e-208">Cela aura un impact particulièrement désastreux si vous possédez des applications qui s’appuient sur les jetons pour exécuter les tâches d’arrière-plan.</span><span class="sxs-lookup"><span data-stu-id="3f78e-208">This is particularly disastrous if you have applications that rely on the tokens to do background work.</span></span> <span data-ttu-id="3f78e-209">Le partage du trousseau nécessite de votre part une précaution infinie avec l’ensemble des opérations de suppression effectuées dans les kits de développement logiciel Microsoft Identity.</span><span class="sxs-lookup"><span data-stu-id="3f78e-209">Sharing a keychain means that you must be very careful in any and all remove operations through the Microsoft Identity SDKs.</span></span>
> 
> 

<span data-ttu-id="3f78e-210">Et voilà !</span><span class="sxs-lookup"><span data-stu-id="3f78e-210">That's it!</span></span> <span data-ttu-id="3f78e-211">Le Kit de développement logiciel (SDK) partage désormais les informations d’identification dans l’ensemble de vos applications.</span><span class="sxs-lookup"><span data-stu-id="3f78e-211">The Microsoft Identity SDK will now share credentials across all your applications.</span></span> <span data-ttu-id="3f78e-212">La liste des utilisateurs sera également partagée entre toutes les instances d’application.</span><span class="sxs-lookup"><span data-stu-id="3f78e-212">The user list will also be shared across application instances.</span></span>

### <a name="turning-on-sso-for-broker-assisted-sso"></a><span data-ttu-id="3f78e-213">Activation de l’authentification unique assistée avec répartiteur</span><span class="sxs-lookup"><span data-stu-id="3f78e-213">Turning on SSO for broker assisted SSO</span></span>
<span data-ttu-id="3f78e-214">La capacité d’une application à utiliser un répartiteur installé sur l’appareil est **désactivée par défaut**.</span><span class="sxs-lookup"><span data-stu-id="3f78e-214">The ability for an application to use any broker that is installed on the device is **turned off by default**.</span></span> <span data-ttu-id="3f78e-215">Pour utiliser votre application avec le répartiteur, vous devez effectuer une configuration supplémentaire et ajouter du code à votre application.</span><span class="sxs-lookup"><span data-stu-id="3f78e-215">In order to use your application with the broker you must do some additional configuration and add some code to your application.</span></span>

<span data-ttu-id="3f78e-216">Voici la procédure à suivre :</span><span class="sxs-lookup"><span data-stu-id="3f78e-216">The steps to follow are:</span></span>

1. <span data-ttu-id="3f78e-217">Activez le mode répartiteur dans votre appel du code d’application vers le Kit de développement logiciel MS.</span><span class="sxs-lookup"><span data-stu-id="3f78e-217">Enable broker mode in your application code's call to the MS SDK.</span></span>
2. <span data-ttu-id="3f78e-218">Établissez un nouvel URI de redirection à fournir à l’application et à votre inscription d’application.</span><span class="sxs-lookup"><span data-stu-id="3f78e-218">Establish a new redirect URI and provide that to both the app and your app registration.</span></span>
3. <span data-ttu-id="3f78e-219">Enregistrez un nouveau schéma d’URL.</span><span class="sxs-lookup"><span data-stu-id="3f78e-219">Registering a URL Scheme.</span></span>
4. <span data-ttu-id="3f78e-220">Prise en charge iOS9 : Ajoutez une autorisation à votre fichier info.plist.</span><span class="sxs-lookup"><span data-stu-id="3f78e-220">iOS9 Support: Add a permission to your info.plist file.</span></span>

#### <a name="step-1-enable-broker-mode-in-your-application"></a><span data-ttu-id="3f78e-221">Étape 1 : Activer le mode répartiteur dans votre application</span><span class="sxs-lookup"><span data-stu-id="3f78e-221">Step 1: Enable broker mode in your application</span></span>
<span data-ttu-id="3f78e-222">La capacité de votre application à utiliser le répartiteur est activée lorsque vous créez le contexte, ou la configuration initiale, de votre objet d’authentification.</span><span class="sxs-lookup"><span data-stu-id="3f78e-222">The ability for your application to use the broker is turned on when you create the "context" or initial setup of your Authentication object.</span></span> <span data-ttu-id="3f78e-223">Pour ce faire, définissez votre type d’informations d’identification dans votre code :</span><span class="sxs-lookup"><span data-stu-id="3f78e-223">You do this by setting your credentials type in your code:</span></span>

```
/*! See the ADCredentialsType enumeration definition for details */
@propertyADCredentialsType credentialsType;
```
<span data-ttu-id="3f78e-224">Le paramètre `AD_CREDENTIALS_AUTO` autorise le Kit de développement logiciel Microsoft Identity à essayer d’appeler le répartiteur, tandis que `AD_CREDENTIALS_EMBEDDED` l’empêche de le faire.</span><span class="sxs-lookup"><span data-stu-id="3f78e-224">The `AD_CREDENTIALS_AUTO` setting will allow the Microsoft Identity SDK to try to call out to the broker, `AD_CREDENTIALS_EMBEDDED` will prevent the Microsoft Identity SDK from calling to the broker.</span></span>

#### <a name="step-2-registering-a-url-scheme"></a><span data-ttu-id="3f78e-225">Étape 2 : Enregistrer un nouveau schéma d’URL.</span><span class="sxs-lookup"><span data-stu-id="3f78e-225">Step 2: Registering a URL Scheme</span></span>
<span data-ttu-id="3f78e-226">La plateforme Microsoft Identity utilise des URL pour appeler le répartiteur, avant de rendre le contrôle à votre application.</span><span class="sxs-lookup"><span data-stu-id="3f78e-226">The Microsoft Identity platform uses URLs to invoke the broker and then return control back to your application.</span></span> <span data-ttu-id="3f78e-227">Pour terminer cet aller-retour, vous devez disposer d’un schéma d’URL inscrit pour votre application et dont la plateforme Microsoft Identity a connaissance.</span><span class="sxs-lookup"><span data-stu-id="3f78e-227">To finish that round trip you need a URL scheme registered for your application that the Microsoft Identity platform will know about.</span></span> <span data-ttu-id="3f78e-228">Il peut s’agir d’un ajout à un autre schéma d’application précédemment inscrit avec votre application.</span><span class="sxs-lookup"><span data-stu-id="3f78e-228">This can be in addition to any other app schemes you may have previously registered with your application.</span></span>

> [!WARNING]
> <span data-ttu-id="3f78e-229">Nous vous recommandons de personnaliser au maximum le schéma d’URL, ceci pour réduire la probabilité qu’une autre application utilise le même schéma d’URL.</span><span class="sxs-lookup"><span data-stu-id="3f78e-229">We recommend making the URL scheme fairly unique to minimize the chances of another app using the same URL scheme.</span></span> <span data-ttu-id="3f78e-230">Apple n’applique pas l’unicité des schémas d’URL inscrits dans le magasin d’applications.</span><span class="sxs-lookup"><span data-stu-id="3f78e-230">Apple does not enforce the uniqueness of URL schemes that are registered in the app store.</span></span>
> 
> 

<span data-ttu-id="3f78e-231">Voici un exemple de l’affichage dans votre configuration de projet.</span><span class="sxs-lookup"><span data-stu-id="3f78e-231">Below is an example of how this appears in your project configuration.</span></span> <span data-ttu-id="3f78e-232">Vous pouvez également définir en XCode :</span><span class="sxs-lookup"><span data-stu-id="3f78e-232">You may also do this in XCode as well:</span></span>

```
<key>CFBundleURLTypes</key>
<array>
    <dict>
        <key>CFBundleTypeRole</key>
        <string>Editor</string>
        <key>CFBundleURLName</key>
        <string>com.myapp.mytestapp</string>
        <key>CFBundleURLSchemes</key>
        <array>
            <string>x-msauth-mytestiosapp</string>
        </array>
    </dict>
</array>
```

#### <a name="step-3-establish-a-new-redirect-uri-with-your-url-scheme"></a><span data-ttu-id="3f78e-233">Étape 3 : Établissez un nouvel URI de redirection avec votre schéma d’URL</span><span class="sxs-lookup"><span data-stu-id="3f78e-233">Step 3: Establish a new redirect URI with your URL Scheme</span></span>
<span data-ttu-id="3f78e-234">Pour garantir que nous renvoyons toujours les jetons d’identification à l’application appropriée, nous devons nous assurer de respecter une procédure de rappel de votre application pouvant être vérifiée par votre système d’exploitation iOS.</span><span class="sxs-lookup"><span data-stu-id="3f78e-234">In order to ensure that we always return the credential tokens to the correct application, we need to make sure we call back to your application in a way that the iOS operating system can verify.</span></span> <span data-ttu-id="3f78e-235">Le système d’exploitation iOS signale aux applications de répartiteur Microsoft l’ID d’offre de l’application appelante.</span><span class="sxs-lookup"><span data-stu-id="3f78e-235">The iOS operating system reports to the Microsoft broker applications the Bundle ID of the application calling it.</span></span> <span data-ttu-id="3f78e-236">Il ne peut pas être falsifié par une application non fiable.</span><span class="sxs-lookup"><span data-stu-id="3f78e-236">This cannot be spoofed by a rogue application.</span></span> <span data-ttu-id="3f78e-237">Par conséquent, nous tirons parti de cette donnée et de l’URI de notre application de répartiteur pour vérifier que les jetons sont renvoyés à l’application appropriée.</span><span class="sxs-lookup"><span data-stu-id="3f78e-237">Therefore, we leverage this along with the URI of our broker application to ensure that the tokens are returned to the correct application.</span></span> <span data-ttu-id="3f78e-238">Nous vous demandons d’établir cet URI de redirection unique dans votre application et de le définir en tant qu’URI de redirection dans notre portail des développeurs.</span><span class="sxs-lookup"><span data-stu-id="3f78e-238">We require you to establish this unique redirect URI both in your application and set as a Redirect URI in our developer portal.</span></span>

<span data-ttu-id="3f78e-239">Votre URI de redirection doit présenter la forme appropriée suivante :</span><span class="sxs-lookup"><span data-stu-id="3f78e-239">Your redirect URI must be in the proper form of:</span></span>

`<app-scheme>://<your.bundle.id>`

<span data-ttu-id="3f78e-240">ex : *x-msauth-mytestiosapp://com.myapp.mytestapp*</span><span class="sxs-lookup"><span data-stu-id="3f78e-240">ex: *x-msauth-mytestiosapp://com.myapp.mytestapp*</span></span>

<span data-ttu-id="3f78e-241">Cet URI de direction doit être spécifié dans l’inscription de votre application avec le [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="3f78e-241">This Redirect URI needs to be specified in your app registration using the [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="3f78e-242">Pour plus d’informations sur l’inscription d’applications Azure AD, consultez [Intégration avec Azure Active Directory](active-directory-how-to-integrate.md).</span><span class="sxs-lookup"><span data-stu-id="3f78e-242">For more information on Azure AD app registration, see [Integrating with Azure Active Directory](active-directory-how-to-integrate.md).</span></span>

##### <a name="step-3a-add-a-redirect-uri-in-your-app-and-dev-portal-to-support-certificate-based-authentication"></a><span data-ttu-id="3f78e-243">Étape 3a : Ajouter un URI de redirection dans votre application et le portail de développement afin de prendre en charge l’authentification par certificat</span><span class="sxs-lookup"><span data-stu-id="3f78e-243">Step 3a: Add a redirect URI in your app and dev portal to support certificate based authentication</span></span>
<span data-ttu-id="3f78e-244">Pour assurer la prise en charge de l’authentification par certificat, vous devez inscrire un second msauth dans votre application et le [portail Azure](https://portal.azure.com/) afin de prendre en charge l’authentification par certificat, si vous souhaitez ajouter cette prise en charge dans votre application.</span><span class="sxs-lookup"><span data-stu-id="3f78e-244">To support cert based authentication a second "msauth"  needs to be registered in your application and the [Azure portal](https://portal.azure.com/) to handle certificate authentication if you wish to add that support in your application.</span></span>

`msauth://code/<broker-redirect-uri-in-url-encoded-form>`

<span data-ttu-id="3f78e-245">exemple : *msauth://code/x-msauth-mytestiosapp%3A%2F%2Fcom.myapp.mytestapp*</span><span class="sxs-lookup"><span data-stu-id="3f78e-245">ex: *msauth://code/x-msauth-mytestiosapp%3A%2F%2Fcom.myapp.mytestapp*</span></span>

#### <a name="step-4-ios9-add-a-configuration-parameter-to-your-app"></a><span data-ttu-id="3f78e-246">Étape 4 : iOS9 : Ajouter un paramètre de configuration à votre application</span><span class="sxs-lookup"><span data-stu-id="3f78e-246">Step 4: iOS9: Add a configuration parameter to your app</span></span>
<span data-ttu-id="3f78e-247">La bibliothèque ADAL utilise –canOpenURL: pour vérifier si le répartiteur est installé sur l’appareil.</span><span class="sxs-lookup"><span data-stu-id="3f78e-247">ADAL uses –canOpenURL: to check if the broker is installed on the device.</span></span> <span data-ttu-id="3f78e-248">Dans iOS 9, Apple a verrouillé la liste des schémas dans lesquels une application peut lancer une requête.</span><span class="sxs-lookup"><span data-stu-id="3f78e-248">In iOS 9 Apple locked down what schemes an application can query for.</span></span> <span data-ttu-id="3f78e-249">Il vous faudra ajouter msauth à la section LSApplicationQueriesSchemes de votre `info.plist file`.</span><span class="sxs-lookup"><span data-stu-id="3f78e-249">You will need to add “msauth” to the LSApplicationQueriesSchemes section of your `info.plist file`.</span></span>

<span data-ttu-id="3f78e-250"><key>LSApplicationQueriesSchemes</key></span><span class="sxs-lookup"><span data-stu-id="3f78e-250"><key>LSApplicationQueriesSchemes</key></span></span>

<span data-ttu-id="3f78e-251"><array><string>msauth</string>
</array></span><span class="sxs-lookup"><span data-stu-id="3f78e-251"><array> <string>msauth</string>
</array></span></span>

### <a name="youve-configured-sso"></a><span data-ttu-id="3f78e-252">Vous avez configuré l’authentification unique !</span><span class="sxs-lookup"><span data-stu-id="3f78e-252">You've configured SSO!</span></span>
<span data-ttu-id="3f78e-253">Désormais, le Kit de développement logiciel (SDK) Microsoft Identity partage automatiquement les informations d’identification entre vos applications et appelle l’éventuel répartiteur existant sur l’appareil.</span><span class="sxs-lookup"><span data-stu-id="3f78e-253">Now the Microsoft Identity SDK will automatically both share credentials across your applications and invoke the broker if it's present on their device.</span></span>

