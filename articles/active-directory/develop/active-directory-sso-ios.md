---
title: "aaaHow tooenable SSO inter-applications sur iOS à l’aide de la bibliothèque ADAL | Documents Microsoft"
description: "Comment toouse les fonctionnalités de hello de hello tooenable SDK ADAL Single Sign On dans vos applications. "
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
ms.openlocfilehash: b7b4389a8dcd956211ffa1aaa431aaf21ded8961
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooenable-cross-app-sso-on-ios-using-adal"></a><span data-ttu-id="90f96-103">Comment tooenable l’authentification unique entre l’application sur iOS à l’aide de la bibliothèque ADAL</span><span class="sxs-lookup"><span data-stu-id="90f96-103">How tooenable cross-app SSO on iOS using ADAL</span></span>
<span data-ttu-id="90f96-104">Fournissant Single Sign-On (SSO) afin que les utilisateurs uniquement besoin de tooenter leurs informations d’identification qu’une seule fois ont ces informations d’identification du travail automatiquement entre les applications est désormais attendu par les clients.</span><span class="sxs-lookup"><span data-stu-id="90f96-104">Providing Single Sign-On (SSO) so that users only need tooenter their credentials once and have those credentials automatically work across applications is now expected by customers.</span></span> <span data-ttu-id="90f96-105">difficulté Hello en entrant leur nom d’utilisateur et un mot de passe sur un petit écran, souvent fois combinés avec un facteur supplémentaire (2FA) comme un appel téléphonique ou un code envoyé par SMS, entraîne le mécontentement rapide si un utilisateur a toodo cela plusieurs fois pour votre produit.</span><span class="sxs-lookup"><span data-stu-id="90f96-105">hello difficulty in entering their username and password on a small screen, often times combined with an additional factor (2FA) like a phone call or a texted code, results in quick dissatisfaction if a user has toodo this more than one time for your product.</span></span>

<span data-ttu-id="90f96-106">En outre, si vous appliquez une plateforme d’identité qui peuvent utiliser des autres applications telles que Microsoft Accounts ou un compte professionnel à partir d’Office 365, les clients attendent que ces toouse disponible de toobe informations d’identification pour toutes les applications de leurs quel que soit le fournisseur de hello.</span><span class="sxs-lookup"><span data-stu-id="90f96-106">In addition, if you apply an identity platform that other applications may use such as Microsoft Accounts or a work account from Office365, customers expect that those credentials toobe available toouse across all their applications no matter hello vendor.</span></span>

<span data-ttu-id="90f96-107">Hello plateforme Microsoft Identity, ainsi que nos kits de développement Microsoft Identity, fait tout ce travail pour vous et donne vous hello toodelight de capacité de vos clients avec l’authentification unique au sein de votre propre suite d’applications ou, en tant que notre service broker et un authentificateur applications, sur l’ensemble de l’unité hello.</span><span class="sxs-lookup"><span data-stu-id="90f96-107">hello Microsoft Identity platform, along with our Microsoft Identity SDKs, does all this hard work for you and gives you hello ability toodelight your customers with SSO either within your own suite of applications or, as with our broker capability and Authenticator applications, across hello entire device.</span></span>

<span data-ttu-id="90f96-108">Cette procédure pas à pas explique comment tooconfigure notre kit de développement logiciel au sein de votre application de tooprovide cet avantage tooyour les clients.</span><span class="sxs-lookup"><span data-stu-id="90f96-108">This walkthrough will tell you how tooconfigure our SDK within your application tooprovide this benefit tooyour customers.</span></span>

<span data-ttu-id="90f96-109">Cette procédure pas à pas s’applique aux éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="90f96-109">This walkthrough applies to:</span></span>

* <span data-ttu-id="90f96-110">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="90f96-110">Azure Active Directory</span></span>
* <span data-ttu-id="90f96-111">Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="90f96-111">Azure Active Directory B2C</span></span>
* <span data-ttu-id="90f96-112">Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="90f96-112">Azure Active Directory B2B</span></span>
* <span data-ttu-id="90f96-113">Accès conditionnel Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="90f96-113">Azure Active Directory Conditional Access</span></span>

<span data-ttu-id="90f96-114">document Hello précédent suppose que vous savez comment trop[la configuration des applications dans le portail hérité de hello pour Azure Active Directory](active-directory-how-to-integrate.md) et d’intégrer votre application hello [Microsoft Identity iOS SDK](https://github.com/AzureAD/azure-activedirectory-library-for-objc).</span><span class="sxs-lookup"><span data-stu-id="90f96-114">hello document preceding assumes you know how too[provision applications in hello legacy portal for Azure Active Directory](active-directory-how-to-integrate.md) and integrated your application with hello [Microsoft Identity iOS SDK](https://github.com/AzureAD/azure-activedirectory-library-for-objc).</span></span>

## <a name="sso-concepts-in-hello-microsoft-identity-platform"></a><span data-ttu-id="90f96-115">Concepts de l’authentification unique Bonjour plateforme d’identité Microsoft</span><span class="sxs-lookup"><span data-stu-id="90f96-115">SSO Concepts in hello Microsoft Identity Platform</span></span>
### <a name="microsoft-identity-brokers"></a><span data-ttu-id="90f96-116">Répartiteurs Microsoft Identity</span><span class="sxs-lookup"><span data-stu-id="90f96-116">Microsoft Identity Brokers</span></span>
<span data-ttu-id="90f96-117">Microsoft fournit des applications pour toutes les plateformes mobiles acceptant pour le pontage hello d’informations d’identification entre les applications provenant de différents fournisseurs et permet à des fonctionnalités améliorées spéciales qui requièrent un seul emplacement sécurisé à partir de laquelle les informations d’identification de toovalidate.</span><span class="sxs-lookup"><span data-stu-id="90f96-117">Microsoft provides applications for every mobile platform that allow for hello bridging of credentials across applications from different vendors and allows for special enhanced features that require a single secure place from where toovalidate credentials.</span></span> <span data-ttu-id="90f96-118">Nous appelons ces applications **répartiteurs**.</span><span class="sxs-lookup"><span data-stu-id="90f96-118">We call these **brokers**.</span></span> <span data-ttu-id="90f96-119">Sur iOS et Android ces courtiers sont fournies via des applications téléchargeables que clients installer indépendamment ou pouvant être envoyées toohello appareil par une société qui gère tout ou partie des périphériques de hello pour leurs employés.</span><span class="sxs-lookup"><span data-stu-id="90f96-119">On iOS and Android these brokers are provided through downloadable applications that customers either install independently or can be pushed toohello device by a company who manages some or all of hello device for their employee.</span></span> <span data-ttu-id="90f96-120">Ces services Broker prend en charge la gestion de la sécurité pour certaines applications ou certains hello ensemble de l’unité selon ce que les administrateurs informatiques souhaitent.</span><span class="sxs-lookup"><span data-stu-id="90f96-120">These brokers support managing security just for some applications or hello entire device based on what IT Administrators desire.</span></span> <span data-ttu-id="90f96-121">Dans Windows, cette fonctionnalité est fournie par un sélecteur de compte de système d’exploitation de toohello, appelé techniquement hello Service Broker d’authentification Web intégré.</span><span class="sxs-lookup"><span data-stu-id="90f96-121">In Windows, this functionality is provided by an account chooser built in toohello operating system, known technically as hello Web Authentication Broker.</span></span>

<span data-ttu-id="90f96-122">Pour plus d’informations sur la façon de nous utilisons ces courtiers et comment vos clients peuvent voir les leur flux de connexion pour la plateforme de Microsoft Identity hello lire sur.</span><span class="sxs-lookup"><span data-stu-id="90f96-122">For more information on how we use these brokers and how your customers might see them in their login flow for hello Microsoft Identity platform read on.</span></span>

### <a name="patterns-for-logging-in-on-mobile-devices"></a><span data-ttu-id="90f96-123">Modèles de connexion sur les appareils mobiles</span><span class="sxs-lookup"><span data-stu-id="90f96-123">Patterns for logging in on mobile devices</span></span>
<span data-ttu-id="90f96-124">Deux modèles de base pour la plateforme de Microsoft Identity hello, procédez toocredentials d’accès sur les appareils :</span><span class="sxs-lookup"><span data-stu-id="90f96-124">Access toocredentials on devices follow two basic patterns for hello Microsoft Identity platform:</span></span>

* <span data-ttu-id="90f96-125">Connexions assistées sans répartiteur</span><span class="sxs-lookup"><span data-stu-id="90f96-125">Non-broker assisted logins</span></span>
* <span data-ttu-id="90f96-126">Connexions assistées avec répartiteur</span><span class="sxs-lookup"><span data-stu-id="90f96-126">Broker assisted logins</span></span>

#### <a name="non-broker-assisted-logins"></a><span data-ttu-id="90f96-127">Connexions assistées sans répartiteur</span><span class="sxs-lookup"><span data-stu-id="90f96-127">Non-broker assisted logins</span></span>
<span data-ttu-id="90f96-128">Non-Service Broker pour les connexions assistées sont les expériences de connexion qui se produisent en ligne avec l’application hello et utilisent le stockage local de hello sur l’appareil hello pour cette application.</span><span class="sxs-lookup"><span data-stu-id="90f96-128">Non-broker assisted logins are login experiences that happen inline with hello application and use hello local storage on hello device for that application.</span></span> <span data-ttu-id="90f96-129">Ce stockage peut être partagé entre les applications, mais les informations d’identification de hello sont étroitement liés toohello application ou la suite d’applications à l’aide de ces informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="90f96-129">This storage may be shared across applications but hello credentials are tightly bound toohello app or suite of apps using that credential.</span></span> <span data-ttu-id="90f96-130">Vous avez probablement rencontré cela dans de nombreuses applications mobiles lorsque vous entrez un nom d’utilisateur et un mot de passe au sein de l’application hello lui-même.</span><span class="sxs-lookup"><span data-stu-id="90f96-130">You've most likely experienced this in many mobile applications when you enter a username and password within hello application itself.</span></span>

<span data-ttu-id="90f96-131">Ces connexions ont hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="90f96-131">These logins have hello following benefits:</span></span>

* <span data-ttu-id="90f96-132">Expérience utilisateur existe entièrement dans l’application hello.</span><span class="sxs-lookup"><span data-stu-id="90f96-132">User experience exists entirely within hello application.</span></span>
* <span data-ttu-id="90f96-133">Informations d’identification peuvent être partagées entre les applications qui sont signées par hello même certificat, en fournissant une suite de tooyour une expérience d’authentification unique d’applications.</span><span class="sxs-lookup"><span data-stu-id="90f96-133">Credentials can be shared across applications that are signed by hello same certificate, providing a single sign-on experience tooyour suite of applications.</span></span>
* <span data-ttu-id="90f96-134">Contrôle autour d’expérience hello de connexion est fourni toohello application avant et après la connexion.</span><span class="sxs-lookup"><span data-stu-id="90f96-134">Control around hello experience of logging in is provided toohello application before and after sign-in.</span></span>

<span data-ttu-id="90f96-135">Ces connexions ont hello suivant des inconvénients :</span><span class="sxs-lookup"><span data-stu-id="90f96-135">These logins have hello following drawbacks:</span></span>

* <span data-ttu-id="90f96-136">L’utilisateur ne peut pas profiter de l’authentification unique sur l’ensemble des applications utilisant Microsoft Identity, uniquement sur celles que votre application a configuré.</span><span class="sxs-lookup"><span data-stu-id="90f96-136">User cannot experience single-sign on across all apps that use a Microsoft Identity, only across those Microsoft Identities that your application has configured.</span></span>
* <span data-ttu-id="90f96-137">Votre application ne peut pas être utilisée avec des fonctionnalités d’entreprise plus avancées telles que l’accès conditionnel ou utilisez hello InTune suite de produits.</span><span class="sxs-lookup"><span data-stu-id="90f96-137">Your application cannot be used with more advanced business features such as Conditional Access or use hello InTune suite of products.</span></span>
* <span data-ttu-id="90f96-138">Votre application ne peut pas prendre en charge l’authentification par certificat des utilisateurs professionnels.</span><span class="sxs-lookup"><span data-stu-id="90f96-138">Your application can't support certificate-based authentication for business users.</span></span>

<span data-ttu-id="90f96-139">Voici une représentation du fonctionnement des kits de développement logiciel hello Microsoft identité avec le stockage de vos tooenable applications SSO hello partagé :</span><span class="sxs-lookup"><span data-stu-id="90f96-139">Here is a representation of how hello Microsoft Identity SDKs work with hello shared storage of your applications tooenable SSO:</span></span>

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

#### <a name="broker-assisted-logins"></a><span data-ttu-id="90f96-140">Connexions assistées avec répartiteur</span><span class="sxs-lookup"><span data-stu-id="90f96-140">Broker assisted logins</span></span>
<span data-ttu-id="90f96-141">Assisté par service Broker pour les connexions sont des expériences de connexion qui se produisent dans l’application de service broker hello et d’utilisent le stockage de hello et la sécurité des informations d’identification de hello broker tooshare sur toutes les applications sur l’appareil de hello qui s’appliquent de plateforme de Microsoft Identity hello.</span><span class="sxs-lookup"><span data-stu-id="90f96-141">Broker-assisted logins are login experiences that occur within hello broker application and use hello storage and security of hello broker tooshare credentials across all applications on hello device that apply hello Microsoft Identity platform.</span></span> <span data-ttu-id="90f96-142">Cela signifie que vos applications hello broker toosign utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="90f96-142">This means that your applications rely on hello broker toosign users in.</span></span> <span data-ttu-id="90f96-143">Sur iOS et Android ces courtiers sont fournies via des applications téléchargeables que clients installer indépendamment ou pouvant être envoyées toohello appareil par une société qui gère le périphérique hello pour leurs utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="90f96-143">On iOS and Android these brokers are provided through downloadable applications that customers either install independently or can be pushed toohello device by a company who manages hello device for their user.</span></span> <span data-ttu-id="90f96-144">Un exemple de ce type d’application est l’application de Microsoft Authenticator hello sur iOS.</span><span class="sxs-lookup"><span data-stu-id="90f96-144">An example of this type of application is hello Microsoft Authenticator application on iOS.</span></span> <span data-ttu-id="90f96-145">Dans Windows, cette fonctionnalité est fournie par un sélecteur de compte de système d’exploitation de toohello, appelé techniquement hello Service Broker d’authentification Web intégré.</span><span class="sxs-lookup"><span data-stu-id="90f96-145">In Windows this functionality is provided by an account chooser built in toohello operating system, known technically as hello Web Authentication Broker.</span></span>
<span data-ttu-id="90f96-146">expérience de Hello varie selon la plate-forme et peut parfois être perturbateur toousers si elle n’est pas géré correctement.</span><span class="sxs-lookup"><span data-stu-id="90f96-146">hello experience varies by platform and can sometimes be disruptive toousers if not managed correctly.</span></span> <span data-ttu-id="90f96-147">Vous connaissez probablement plus ce modèle si vous disposez d’application Facebook hello et utilisez la connexion à Facebook à partir d’une autre application.</span><span class="sxs-lookup"><span data-stu-id="90f96-147">You're probably most familiar with this pattern if you have hello Facebook application installed and use Facebook Connect from another application.</span></span> <span data-ttu-id="90f96-148">Hello utilise de plateforme d’identité Microsoft hello même modèle.</span><span class="sxs-lookup"><span data-stu-id="90f96-148">hello Microsoft Identity platform uses hello same pattern.</span></span>

<span data-ttu-id="90f96-149">Pour iOS cela entraîne l’animation tooa « transition » où votre application est envoyée arrière-plan toohello lors des applications de Microsoft Authenticator hello est fourni au premier plan toohello pour hello utilisateur tooselect quel compte il veut toosign avec.</span><span class="sxs-lookup"><span data-stu-id="90f96-149">For iOS this leads tooa "transition" animation where your application is sent toohello background while hello Microsoft Authenticator applications comes toohello foreground for hello user tooselect which account they would like toosign in with.</span></span>  

<span data-ttu-id="90f96-150">Pour le compte de hello Android et Windows sélecteur s’affiche au-dessus de votre application qui est moins toohello utilisateur.</span><span class="sxs-lookup"><span data-stu-id="90f96-150">For Android and Windows hello account chooser is displayed on top of your application which is less disruptive toohello user.</span></span>

#### <a name="how-hello-broker-gets-invoked"></a><span data-ttu-id="90f96-151">Comment le service broker de hello appelée</span><span class="sxs-lookup"><span data-stu-id="90f96-151">How hello broker gets invoked</span></span>
<span data-ttu-id="90f96-152">Si un service broker compatible est installé sur le périphérique hello, comme hello application Microsoft Authenticator, hello kits de développement logiciel de Microsoft Identity sera automatiquement hello travail d’un appel de broker hello pour vous quand un utilisateur indique qu’ils souhaitent toolog à l’aide de n’importe quel compte de plateforme de Microsoft Identity Hello.</span><span class="sxs-lookup"><span data-stu-id="90f96-152">If a compatible broker is installed on hello device, like hello Microsoft Authenticator application, hello Microsoft Identity SDKs will automatically do hello work of invoking hello broker for you when a user indicates they wish toolog in using any account from hello Microsoft Identity platform.</span></span> <span data-ttu-id="90f96-153">Il peut s’agir d’un compte personnel Microsoft, d’un compte professionnel ou scolaire, ou d’un compte que vous fournissez et hébergez dans Microsoft Azure à l’aide de nos produits B2C et B2B.</span><span class="sxs-lookup"><span data-stu-id="90f96-153">This account could be a personal Microsoft Account, a work or school account, or an account that you provide and host in Azure using our B2C and B2B products.</span></span> 

 #### <a name="how-we-ensure-hello-application-is-valid"></a><span data-ttu-id="90f96-154">Comment nous assurer l’application hello est valide</span><span class="sxs-lookup"><span data-stu-id="90f96-154">How we ensure hello application is valid</span></span>
 
 <span data-ttu-id="90f96-155">identité de hello tooensure Hello besoin d’un service Broker pour les applications appel hello est sécurité essentielle toohello que nous fournir dans les connexions de broker assistée.</span><span class="sxs-lookup"><span data-stu-id="90f96-155">hello need tooensure hello identity of an application call hello broker is crucial toohello security we provide in broker assisted logins.</span></span> <span data-ttu-id="90f96-156">IOS, ni Android applique des identificateurs uniques qui sont valides uniquement pour une application donnée, afin que des applications malveillantes peuvent « usurper l’identité « identificateur d’une application légitime et recevoir des jetons hello destinées à être application légitime hello.</span><span class="sxs-lookup"><span data-stu-id="90f96-156">Neither iOS nor Android enforces unique identifiers that are valid only for a given application, so malicious applications may "spoof" a legitimate application's identifier and receive hello tokens meant for hello legitimate application.</span></span> <span data-ttu-id="90f96-157">tooensure que nous communiquons toujours avec application droite hello lors de l’exécution, nous vous demandons hello développeur tooprovide un redirectURI personnalisé lors de l’inscription de leur application auprès de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="90f96-157">tooensure we are always communicating with hello right application at runtime, we ask hello developer tooprovide a custom redirectURI when registering their application with Microsoft.</span></span> <span data-ttu-id="90f96-158">**Nous expliquons ci-dessous comment les développeurs doivent créer cet URI de redirection.**</span><span class="sxs-lookup"><span data-stu-id="90f96-158">**How developers should craft this redirect URI is discussed in detail below.**</span></span> <span data-ttu-id="90f96-159">Cette redirectURI personnalisé contient hello ID d’offre groupée de l’application hello et assurer toobe toohello unique application hello Apple App Store.</span><span class="sxs-lookup"><span data-stu-id="90f96-159">This custom redirectURI contains hello Bundle ID of hello application and is ensured toobe unique toohello application by hello Apple App Store.</span></span> <span data-ttu-id="90f96-160">Lorsqu’un broker hello appels d’application, service broker de hello pose hello iOS tooprovide de système de fonctionnement avec hello ID d’offre groupée qui a appelé le service broker de hello.</span><span class="sxs-lookup"><span data-stu-id="90f96-160">When an application calls hello broker, hello broker asks hello iOS operating system tooprovide it with hello Bundle ID that called hello broker.</span></span> <span data-ttu-id="90f96-161">service broker de Hello fournit cette tooMicrosoft ID d’offre groupée dans le système d’identité tooour hello appel.</span><span class="sxs-lookup"><span data-stu-id="90f96-161">hello broker provides this Bundle ID tooMicrosoft in hello call tooour identity system.</span></span> <span data-ttu-id="90f96-162">Si hello ID d’offre groupée de l’application hello ne correspond pas hello QU'ID d’offre groupée fourni toous par le développeur de hello lors de l’inscription, nous refuse l’accès toohello jetons pour l’application hello ressource hello demande.</span><span class="sxs-lookup"><span data-stu-id="90f96-162">If hello Bundle ID of hello application does not match hello Bundle ID provided toous by hello developer during registration, we will deny access toohello tokens for hello resource hello application is requesting.</span></span> <span data-ttu-id="90f96-163">Cette vérification ne garantit que les application hello enregistrées par le développeur de hello reçoit les jetons.</span><span class="sxs-lookup"><span data-stu-id="90f96-163">This check ensures that only hello application registered by hello developer receives tokens.</span></span>

<span data-ttu-id="90f96-164">**développeur de Hello a choix entre hello si hello Kit de développement logiciel de Microsoft Identity appelle le service broker de hello ou agira hello non broker assistée.**</span><span class="sxs-lookup"><span data-stu-id="90f96-164">**hello developer has hello choice of if hello Microsoft Identity SDK calls hello broker or uses hello non-broker assisted flow.**</span></span> <span data-ttu-id="90f96-165">Toutefois si le développeur de hello ne choisit pas de flux d’assisté par service broker de hello toouse ils plus hello à l’aide des informations d’identification de l’authentification unique que l’utilisateur hello a peut-être déjà ajouté sur le périphérique de hello et empêche leur application d’être utilisés avec les fonctionnalités d’entreprise Microsoft fournit à ses clients, tels que l’accès conditionnel, les fonctionnalités de gestion Intune et l’authentification par certificat.</span><span class="sxs-lookup"><span data-stu-id="90f96-165">However if hello developer chooses not toouse hello broker-assisted flow they lose hello benefit of using SSO credentials that hello user may have already added on hello device and prevents their application from being used with business features Microsoft provides its customers such as Conditional Access, Intune Management capabilities, and certificate-based authentication.</span></span>

<span data-ttu-id="90f96-166">Ces connexions ont hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="90f96-166">These logins have hello following benefits:</span></span>

* <span data-ttu-id="90f96-167">Utilisateur rencontre l’authentification unique sur toutes leurs applications, quel que soit le fournisseur de hello.</span><span class="sxs-lookup"><span data-stu-id="90f96-167">User experiences SSO across all their applications no matter hello vendor.</span></span>
* <span data-ttu-id="90f96-168">Votre application peut utiliser les fonctionnalités d’entreprise plus avancées telles que l’accès conditionnel ou utiliser suite, InTune hello de produits.</span><span class="sxs-lookup"><span data-stu-id="90f96-168">Your application can use more advanced business features such as Conditional Access or use hello InTune suite of products.</span></span>
* <span data-ttu-id="90f96-169">Votre application peut prendre en charge l’authentification par certificat des utilisateurs professionnels.</span><span class="sxs-lookup"><span data-stu-id="90f96-169">Your application can support certificate-based authentication for business users.</span></span>
* <span data-ttu-id="90f96-170">Connectez-vous beaucoup plus sûre expérience comme identité hello de l’application hello et l’utilisateur de hello sont vérifiées par application de service broker hello avec chiffrement et les algorithmes de sécurité supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="90f96-170">Much more secure sign-in experience as hello identity of hello application and hello user are verified by hello broker application with additional security algorithms and encryption.</span></span>

<span data-ttu-id="90f96-171">Ces connexions ont hello suivant des inconvénients :</span><span class="sxs-lookup"><span data-stu-id="90f96-171">These logins have hello following drawbacks:</span></span>

* <span data-ttu-id="90f96-172">Dans iOS utilisateur de hello est passée en dehors de l’expérience de votre application pendant que les informations d’identification sont choisies.</span><span class="sxs-lookup"><span data-stu-id="90f96-172">In iOS hello user is transitioned out of your application's experience while credentials are chosen.</span></span>
* <span data-ttu-id="90f96-173">Perte de connexion de hello hello capacité toomanage expérience pour vos clients dans votre application.</span><span class="sxs-lookup"><span data-stu-id="90f96-173">Loss of hello ability toomanage hello login experience for your customers within your application.</span></span>

<span data-ttu-id="90f96-174">Voici une représentation sous forme de comment utiliser kits de développement logiciel de Microsoft Identity hello hello broker applications tooenable l’authentification unique :</span><span class="sxs-lookup"><span data-stu-id="90f96-174">Here is a representation of how hello Microsoft Identity SDKs work with hello broker applications tooenable SSO:</span></span>

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

<span data-ttu-id="90f96-175">Grâce à ces informations en arrière-plan, vous devez être en mesure de toobetter comprendre et à implémenter l’authentification unique au sein de votre application à l’aide de la plateforme de Microsoft Identity hello et kits de développement logiciel.</span><span class="sxs-lookup"><span data-stu-id="90f96-175">Armed with this background information you should be able toobetter understand and implement SSO within your application using hello Microsoft Identity platform and SDKs.</span></span>

## <a name="enabling-cross-app-sso-using-adal"></a><span data-ttu-id="90f96-176">Activation de l’authentification unique entre applications à l’aide de la bibliothèque ADAL</span><span class="sxs-lookup"><span data-stu-id="90f96-176">Enabling cross-app SSO using ADAL</span></span>
<span data-ttu-id="90f96-177">Nous utilisons ici hello, iOS ADAL Kit de développement logiciel pour :</span><span class="sxs-lookup"><span data-stu-id="90f96-177">Here we use hello ADAL iOS SDK to:</span></span>

* <span data-ttu-id="90f96-178">Activer l’authentification unique assistée sans répartiteur pour votre suite d’applications</span><span class="sxs-lookup"><span data-stu-id="90f96-178">Turn on non-broker assisted SSO for your suite of apps</span></span>
* <span data-ttu-id="90f96-179">Activer la prise en charge de l’authentification unique assistée avec répartiteur</span><span class="sxs-lookup"><span data-stu-id="90f96-179">Turn on support for broker-assisted SSO</span></span>

### <a name="turning-on-sso-for-non-broker-assisted-sso"></a><span data-ttu-id="90f96-180">Activation de l’authentification unique assistée sans répartiteur</span><span class="sxs-lookup"><span data-stu-id="90f96-180">Turning on SSO for non-broker assisted SSO</span></span>
<span data-ttu-id="90f96-181">Pour l’authentification unique assistée de non broker entre les applications hello kits de développement logiciel de Microsoft Identity gèrent une grande partie de la complexité de hello de l’authentification unique pour vous.</span><span class="sxs-lookup"><span data-stu-id="90f96-181">For non-broker assisted SSO across applications hello Microsoft Identity SDKs manage much of hello complexity of SSO for you.</span></span> <span data-ttu-id="90f96-182">Cela inclut la recherche d’utilisateur hello dans le cache de hello et en conservant une liste des utilisateurs connectés pour vous tooquery.</span><span class="sxs-lookup"><span data-stu-id="90f96-182">This includes finding hello right user in hello cache and maintaining a list of logged in users for you tooquery.</span></span>

<span data-ttu-id="90f96-183">tooenable l’authentification unique entre les applications que vous possédez que vous devez hello toodo suivant :</span><span class="sxs-lookup"><span data-stu-id="90f96-183">tooenable SSO across applications you own you need toodo hello following:</span></span>

1. <span data-ttu-id="90f96-184">Vérifiez tous les votre hello d’utilisateur d’applications même ID de Client ou l’ID d’Application.</span><span class="sxs-lookup"><span data-stu-id="90f96-184">Ensure all your applications user hello same Client ID or Application ID.</span></span>
2. <span data-ttu-id="90f96-185">Vérifiez que tous vos hello de partage applications certificat de signature du même auprès d’Apple afin que vous pouvez partager de trousseau</span><span class="sxs-lookup"><span data-stu-id="90f96-185">Ensure that all of your applications share hello same signing certificate from Apple so that you can share keychains</span></span>
3. <span data-ttu-id="90f96-186">Demande hello même droit trousseau pour chacun de vos applications.</span><span class="sxs-lookup"><span data-stu-id="90f96-186">Request hello same keychain entitlement for each of your applications.</span></span>
4. <span data-ttu-id="90f96-187">Précisez kits de développement logiciel hello Microsoft Identity sur hello partagé trousseau nous toouse.</span><span class="sxs-lookup"><span data-stu-id="90f96-187">Tell hello Microsoft Identity SDKs about hello shared keychain you want us toouse.</span></span>

#### <a name="using-hello-same-client-id--application-id-for-all-hello-applications-in-your-suite-of-apps"></a><span data-ttu-id="90f96-188">À l’aide de hello le même ID de Client / ID de l’Application pour tous les hello dans votre ensemble d’applications</span><span class="sxs-lookup"><span data-stu-id="90f96-188">Using hello same Client ID / Application ID for all hello applications in your suite of apps</span></span>
<span data-ttu-id="90f96-189">Par ordre de hello Microsoft Identity plateforme tooknow qu’il est autorisé tooshare jetons dans vos applications, chacune de vos applications devez hello tooshare même ID de Client ou l’ID d’Application.</span><span class="sxs-lookup"><span data-stu-id="90f96-189">In order for hello Microsoft Identity platform tooknow that it's allowed tooshare tokens across your applications, each of your applications will need tooshare hello same Client ID or Application ID.</span></span> <span data-ttu-id="90f96-190">Il s’agit d’identificateur hello qui a été fourni tooyou lorsque vous avez inscrit votre première application dans le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="90f96-190">This is hello unique identifier that was provided tooyou when you registered your first application in hello portal.</span></span>

<span data-ttu-id="90f96-191">Vous vous demandez peut-être comment vous allez identifier les différentes applications toohello service Microsoft Identity s’il utilise hello même ID d’Application.</span><span class="sxs-lookup"><span data-stu-id="90f96-191">You may be wondering how you will identify different apps toohello Microsoft Identity service if it uses hello same Application ID.</span></span> <span data-ttu-id="90f96-192">les réponses Hello sont avec hello **URI de redirection**.</span><span class="sxs-lookup"><span data-stu-id="90f96-192">hello answer is with hello **Redirect URIs**.</span></span> <span data-ttu-id="90f96-193">Chaque application peut avoir plusieurs URI de redirection inscrit dans le portail de l’intégration de hello.</span><span class="sxs-lookup"><span data-stu-id="90f96-193">Each application can have multiple Redirect URIs registered in hello onboarding portal.</span></span> <span data-ttu-id="90f96-194">Chacune des applications de votre suite présente un URI de redirection propre.</span><span class="sxs-lookup"><span data-stu-id="90f96-194">Each app in your suite will have a different redirect URI.</span></span> <span data-ttu-id="90f96-195">Voici une représentation possible :</span><span class="sxs-lookup"><span data-stu-id="90f96-195">An example of how this looks is below:</span></span>

<span data-ttu-id="90f96-196">URI de redirection App1 : `x-msauth-mytestiosapp://com.myapp.mytestapp`</span><span class="sxs-lookup"><span data-stu-id="90f96-196">App1 Redirect URI: `x-msauth-mytestiosapp://com.myapp.mytestapp`</span></span>

<span data-ttu-id="90f96-197">URI de redirection App2 : `x-msauth-mytestiosapp://com.myapp.mytestapp2`</span><span class="sxs-lookup"><span data-stu-id="90f96-197">App2 Redirect URI: `x-msauth-mytestiosapp://com.myapp.mytestapp2`</span></span>

<span data-ttu-id="90f96-198">URI de redirection App3 : `x-msauth-mytestiosapp://com.myapp.mytestapp3`</span><span class="sxs-lookup"><span data-stu-id="90f96-198">App3 Redirect URI: `x-msauth-mytestiosapp://com.myapp.mytestapp3`</span></span>

<span data-ttu-id="90f96-199">....</span><span class="sxs-lookup"><span data-stu-id="90f96-199">....</span></span>

<span data-ttu-id="90f96-200">Elles sont imbriquées sous hello même ID de client / ID d’application et recherchée hello en fonction de redirection URI vous renvoyer toous dans votre configuration du Kit de développement logiciel.</span><span class="sxs-lookup"><span data-stu-id="90f96-200">These are nested under hello same client ID / application ID and looked up based on hello redirect URI you return toous in your SDK configuration.</span></span>

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


<span data-ttu-id="90f96-201">*Notez que le format de ces URI de redirection de hello sont expliquées ci-dessous. Vous pouvez utiliser n’importe quel URI de redirection, sauf si vous le souhaitez broker de hello toosupport, auquel cas ils doivent ressembler à hello ci-dessus*</span><span class="sxs-lookup"><span data-stu-id="90f96-201">*Note that hello format of these Redirect URIs are explained below. You may use any Redirect URI unless you wish toosupport hello broker, in which case they must look something like hello above*</span></span>

#### <a name="create-keychain-sharing-between-applications"></a><span data-ttu-id="90f96-202">Créer le partage de trousseau entre les applications</span><span class="sxs-lookup"><span data-stu-id="90f96-202">Create keychain sharing between applications</span></span>
<span data-ttu-id="90f96-203">Activation du partage de trousseau est abordée dans ce document hello et traitées par Apple dans leur document [Adding Capabilities](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html).</span><span class="sxs-lookup"><span data-stu-id="90f96-203">Enabling keychain sharing is beyond hello scope of this document and covered by Apple in their document [Adding Capabilities](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html).</span></span> <span data-ttu-id="90f96-204">L’essentiel est que vous décidez que votre toobe trousseau appelée et ajoutez cette fonctionnalité dans toutes vos applications.</span><span class="sxs-lookup"><span data-stu-id="90f96-204">What is important is that you decide what you want your keychain toobe called and add that capability across all your applications.</span></span>

<span data-ttu-id="90f96-205">Lorsque vous avez droits configurés correctement, vous devraient voir un fichier dans votre répertoire de projet intitulée `entitlements.plist` contenant quelque chose ressemblant à hello suivantes :</span><span class="sxs-lookup"><span data-stu-id="90f96-205">When you do have entitlements set up correctly you should see a file in your project directory entitled `entitlements.plist` that contains something that looks like hello following:</span></span>

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

<span data-ttu-id="90f96-206">Une fois que vous avez les droits de trousseau hello activée dans chacune de vos applications, et vous êtes prêt toouse SSO, informer hello Kit de développement logiciel de Microsoft Identity votre trousseau à l’aide de hello suivant paramètre dans votre `ADAuthenticationSettings` avec hello suivant paramètre :</span><span class="sxs-lookup"><span data-stu-id="90f96-206">Once you have hello keychain entitlement enabled in each of your applications, and you are ready toouse SSO, tell hello Microsoft Identity SDK about your keychain by using hello following setting in your `ADAuthenticationSettings` with hello following setting:</span></span>

```
defaultKeychainSharingGroup=@"com.myapp.mycache";
```

> [!WARNING]
> <span data-ttu-id="90f96-207">Lorsque vous partagez un trousseau dans vos applications n’importe quelle application peut supprimer des utilisateurs ou pire supprimer tous les jetons hello dans votre application.</span><span class="sxs-lookup"><span data-stu-id="90f96-207">When you share a keychain across your applications any application can delete users or worse delete all hello tokens across your application.</span></span> <span data-ttu-id="90f96-208">Cela est particulièrement désastreux si vous avez des applications qui reposent sur le travail d’arrière-plan toodo hello jetons.</span><span class="sxs-lookup"><span data-stu-id="90f96-208">This is particularly disastrous if you have applications that rely on hello tokens toodo background work.</span></span> <span data-ttu-id="90f96-209">Partage un trousseau signifie que vous devez être très prudent dans toutes les supprime les opérations via le SDK d’identité Microsoft hello.</span><span class="sxs-lookup"><span data-stu-id="90f96-209">Sharing a keychain means that you must be very careful in any and all remove operations through hello Microsoft Identity SDKs.</span></span>
> 
> 

<span data-ttu-id="90f96-210">Et voilà !</span><span class="sxs-lookup"><span data-stu-id="90f96-210">That's it!</span></span> <span data-ttu-id="90f96-211">Hello Kit de développement logiciel de Microsoft Identity partagent maintenant informations d’identification dans toutes vos applications.</span><span class="sxs-lookup"><span data-stu-id="90f96-211">hello Microsoft Identity SDK will now share credentials across all your applications.</span></span> <span data-ttu-id="90f96-212">liste des utilisateurs Hello est également partagé entre les instances de l’application.</span><span class="sxs-lookup"><span data-stu-id="90f96-212">hello user list will also be shared across application instances.</span></span>

### <a name="turning-on-sso-for-broker-assisted-sso"></a><span data-ttu-id="90f96-213">Activation de l’authentification unique assistée avec répartiteur</span><span class="sxs-lookup"><span data-stu-id="90f96-213">Turning on SSO for broker assisted SSO</span></span>
<span data-ttu-id="90f96-214">Hello possibilité pour un toouse de l’application est de n’importe quel service broker qui est installé sur l’appareil de hello **désactivée par défaut**.</span><span class="sxs-lookup"><span data-stu-id="90f96-214">hello ability for an application toouse any broker that is installed on hello device is **turned off by default**.</span></span> <span data-ttu-id="90f96-215">Dans commande toouse votre application avec le service broker de hello, vous devez effectuer une configuration supplémentaire et ajouter une application tooyour de code.</span><span class="sxs-lookup"><span data-stu-id="90f96-215">In order toouse your application with hello broker you must do some additional configuration and add some code tooyour application.</span></span>

<span data-ttu-id="90f96-216">Hello étapes toofollow sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="90f96-216">hello steps toofollow are:</span></span>

1. <span data-ttu-id="90f96-217">Activer le mode de service broker dans toohello d’appel de code de votre application MS SDK.</span><span class="sxs-lookup"><span data-stu-id="90f96-217">Enable broker mode in your application code's call toohello MS SDK.</span></span>
2. <span data-ttu-id="90f96-218">Établir un nouveau URI de redirection et fournir cette application de hello tooboth et inscription de votre application.</span><span class="sxs-lookup"><span data-stu-id="90f96-218">Establish a new redirect URI and provide that tooboth hello app and your app registration.</span></span>
3. <span data-ttu-id="90f96-219">Enregistrez un nouveau schéma d’URL.</span><span class="sxs-lookup"><span data-stu-id="90f96-219">Registering a URL Scheme.</span></span>
4. <span data-ttu-id="90f96-220">prise en charge iOS9 : ajouter un fichier info.plist de tooyour autorisation.</span><span class="sxs-lookup"><span data-stu-id="90f96-220">iOS9 Support: Add a permission tooyour info.plist file.</span></span>

#### <a name="step-1-enable-broker-mode-in-your-application"></a><span data-ttu-id="90f96-221">Étape 1 : Activer le mode répartiteur dans votre application</span><span class="sxs-lookup"><span data-stu-id="90f96-221">Step 1: Enable broker mode in your application</span></span>
<span data-ttu-id="90f96-222">possibilité de Hello pour votre courtier de hello toouse application est activée lorsque vous créez le « contexte de hello » ou la configuration initiale de votre objet d’authentification.</span><span class="sxs-lookup"><span data-stu-id="90f96-222">hello ability for your application toouse hello broker is turned on when you create hello "context" or initial setup of your Authentication object.</span></span> <span data-ttu-id="90f96-223">Pour ce faire, définissez votre type d’informations d’identification dans votre code :</span><span class="sxs-lookup"><span data-stu-id="90f96-223">You do this by setting your credentials type in your code:</span></span>

```
/*! See hello ADCredentialsType enumeration definition for details */
@propertyADCredentialsType credentialsType;
```
<span data-ttu-id="90f96-224">Hello `AD_CREDENTIALS_AUTO` permettra de hello Kit de développement logiciel de Microsoft Identity tootry toocall hors toohello broker, `AD_CREDENTIALS_EMBEDDED` empêchera hello Kit de développement logiciel de Microsoft Identity appelant toohello broker.</span><span class="sxs-lookup"><span data-stu-id="90f96-224">hello `AD_CREDENTIALS_AUTO` setting will allow hello Microsoft Identity SDK tootry toocall out toohello broker, `AD_CREDENTIALS_EMBEDDED` will prevent hello Microsoft Identity SDK from calling toohello broker.</span></span>

#### <a name="step-2-registering-a-url-scheme"></a><span data-ttu-id="90f96-225">Étape 2 : Enregistrer un nouveau schéma d’URL.</span><span class="sxs-lookup"><span data-stu-id="90f96-225">Step 2: Registering a URL Scheme</span></span>
<span data-ttu-id="90f96-226">plateforme de Microsoft Identity Hello utilise Service Broker pour les URL tooinvoke hello et contrôle puis retour arrière tooyour application.</span><span class="sxs-lookup"><span data-stu-id="90f96-226">hello Microsoft Identity platform uses URLs tooinvoke hello broker and then return control back tooyour application.</span></span> <span data-ttu-id="90f96-227">toofinish que vous avez besoin d’un modèle d’URL complet inscrit pour votre application que Microsoft Identity connaître plateforme hello.</span><span class="sxs-lookup"><span data-stu-id="90f96-227">toofinish that round trip you need a URL scheme registered for your application that hello Microsoft Identity platform will know about.</span></span> <span data-ttu-id="90f96-228">Cela peut être également tooany autres schémas d’application vous pouvez avoir précédemment inscrits avec votre application.</span><span class="sxs-lookup"><span data-stu-id="90f96-228">This can be in addition tooany other app schemes you may have previously registered with your application.</span></span>

> [!WARNING]
> <span data-ttu-id="90f96-229">Nous vous recommandons de donner hello URL schéma unique toominimize hello risques qu’une autre application à l’aide de hello même schéma d’URL.</span><span class="sxs-lookup"><span data-stu-id="90f96-229">We recommend making hello URL scheme fairly unique toominimize hello chances of another app using hello same URL scheme.</span></span> <span data-ttu-id="90f96-230">Apple n’assure pas l’unicité de hello de schémas d’URL qui sont inscrits dans le magasin d’applications hello.</span><span class="sxs-lookup"><span data-stu-id="90f96-230">Apple does not enforce hello uniqueness of URL schemes that are registered in hello app store.</span></span>
> 
> 

<span data-ttu-id="90f96-231">Voici un exemple de l’affichage dans votre configuration de projet.</span><span class="sxs-lookup"><span data-stu-id="90f96-231">Below is an example of how this appears in your project configuration.</span></span> <span data-ttu-id="90f96-232">Vous pouvez également définir en XCode :</span><span class="sxs-lookup"><span data-stu-id="90f96-232">You may also do this in XCode as well:</span></span>

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

#### <a name="step-3-establish-a-new-redirect-uri-with-your-url-scheme"></a><span data-ttu-id="90f96-233">Étape 3 : Établissez un nouvel URI de redirection avec votre schéma d’URL</span><span class="sxs-lookup"><span data-stu-id="90f96-233">Step 3: Establish a new redirect URI with your URL Scheme</span></span>
<span data-ttu-id="90f96-234">Tooensure de commande que nous retournent toujours les informations d’identification de hello jetons toohello une bonne application, nous devons toomake que nous rappeler tooyour l’application d’une manière qui hello du système d’exploitation iOS peut vérifier.</span><span class="sxs-lookup"><span data-stu-id="90f96-234">In order tooensure that we always return hello credential tokens toohello correct application, we need toomake sure we call back tooyour application in a way that hello iOS operating system can verify.</span></span> <span data-ttu-id="90f96-235">système d’exploitation Hello iOS rapports toohello des applications Microsoft broker hello ID d’offre groupée d’application hello appeler.</span><span class="sxs-lookup"><span data-stu-id="90f96-235">hello iOS operating system reports toohello Microsoft broker applications hello Bundle ID of hello application calling it.</span></span> <span data-ttu-id="90f96-236">Il ne peut pas être falsifié par une application non fiable.</span><span class="sxs-lookup"><span data-stu-id="90f96-236">This cannot be spoofed by a rogue application.</span></span> <span data-ttu-id="90f96-237">Par conséquent, nous offrent cette possibilité avec hello URI de notre tooensure d’application de service broker que les jetons de hello sont retournés toohello une bonne application.</span><span class="sxs-lookup"><span data-stu-id="90f96-237">Therefore, we leverage this along with hello URI of our broker application tooensure that hello tokens are returned toohello correct application.</span></span> <span data-ttu-id="90f96-238">Nous avons besoin de vous tooestablish cette redirection unique URI à la fois dans votre application et la définir en tant qu’URI de redirection dans notre portail des développeurs.</span><span class="sxs-lookup"><span data-stu-id="90f96-238">We require you tooestablish this unique redirect URI both in your application and set as a Redirect URI in our developer portal.</span></span>

<span data-ttu-id="90f96-239">Votre URI de redirection doit être de forme correcte hello :</span><span class="sxs-lookup"><span data-stu-id="90f96-239">Your redirect URI must be in hello proper form of:</span></span>

`<app-scheme>://<your.bundle.id>`

<span data-ttu-id="90f96-240">ex : *x-msauth-mytestiosapp://com.myapp.mytestapp*</span><span class="sxs-lookup"><span data-stu-id="90f96-240">ex: *x-msauth-mytestiosapp://com.myapp.mytestapp*</span></span>

<span data-ttu-id="90f96-241">Cet URI de redirection doit toobe spécifié dans votre inscription d’une application à l’aide de hello [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="90f96-241">This Redirect URI needs toobe specified in your app registration using hello [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="90f96-242">Pour plus d’informations sur l’inscription d’applications Azure AD, consultez [Intégration avec Azure Active Directory](active-directory-how-to-integrate.md).</span><span class="sxs-lookup"><span data-stu-id="90f96-242">For more information on Azure AD app registration, see [Integrating with Azure Active Directory](active-directory-how-to-integrate.md).</span></span>

##### <a name="step-3a-add-a-redirect-uri-in-your-app-and-dev-portal-toosupport-certificate-based-authentication"></a><span data-ttu-id="90f96-243">Étape 3 a : ajouter un URI de redirection dans votre application et développement toosupport portail basée sur certificat l’authentification</span><span class="sxs-lookup"><span data-stu-id="90f96-243">Step 3a: Add a redirect URI in your app and dev portal toosupport certificate based authentication</span></span>
<span data-ttu-id="90f96-244">authentification de certificat en fonction de toosupport une deuxième « msauth » doit toobe inscrit dans votre application et de hello [portail Azure](https://portal.azure.com/) toohandle l’authentification du certificat si vous le souhaitez tooadd prenant en charge dans votre application.</span><span class="sxs-lookup"><span data-stu-id="90f96-244">toosupport cert based authentication a second "msauth"  needs toobe registered in your application and hello [Azure portal](https://portal.azure.com/) toohandle certificate authentication if you wish tooadd that support in your application.</span></span>

`msauth://code/<broker-redirect-uri-in-url-encoded-form>`

<span data-ttu-id="90f96-245">exemple : *msauth://code/x-msauth-mytestiosapp%3A%2F%2Fcom.myapp.mytestapp*</span><span class="sxs-lookup"><span data-stu-id="90f96-245">ex: *msauth://code/x-msauth-mytestiosapp%3A%2F%2Fcom.myapp.mytestapp*</span></span>

#### <a name="step-4-ios9-add-a-configuration-parameter-tooyour-app"></a><span data-ttu-id="90f96-246">Étape 4 : iOS9 : ajout d’une application de tooyour de paramètre de configuration</span><span class="sxs-lookup"><span data-stu-id="90f96-246">Step 4: iOS9: Add a configuration parameter tooyour app</span></span>
<span data-ttu-id="90f96-247">La bibliothèque ADAL utilise – canOpenURL : toocheck si service broker de hello est installé sur l’appareil de hello.</span><span class="sxs-lookup"><span data-stu-id="90f96-247">ADAL uses –canOpenURL: toocheck if hello broker is installed on hello device.</span></span> <span data-ttu-id="90f96-248">Dans iOS 9, Apple a verrouillé la liste des schémas dans lesquels une application peut lancer une requête.</span><span class="sxs-lookup"><span data-stu-id="90f96-248">In iOS 9 Apple locked down what schemes an application can query for.</span></span> <span data-ttu-id="90f96-249">Vous devez tooadd « msauth » toohello LSApplicationQueriesSchemes section de votre `info.plist file`.</span><span class="sxs-lookup"><span data-stu-id="90f96-249">You will need tooadd “msauth” toohello LSApplicationQueriesSchemes section of your `info.plist file`.</span></span>

<span data-ttu-id="90f96-250"><key>LSApplicationQueriesSchemes</key></span><span class="sxs-lookup"><span data-stu-id="90f96-250"><key>LSApplicationQueriesSchemes</key></span></span>

<span data-ttu-id="90f96-251"><array><string>msauth</string>
</array></span><span class="sxs-lookup"><span data-stu-id="90f96-251"><array> <string>msauth</string>
</array></span></span>

### <a name="youve-configured-sso"></a><span data-ttu-id="90f96-252">Vous avez configuré l’authentification unique !</span><span class="sxs-lookup"><span data-stu-id="90f96-252">You've configured SSO!</span></span>
<span data-ttu-id="90f96-253">Maintenant hello Kit de développement logiciel de Microsoft Identity automatiquement à la fois partager des informations d’identification entre vos applications et appeler le service broker de hello si elle est présente sur leur appareil.</span><span class="sxs-lookup"><span data-stu-id="90f96-253">Now hello Microsoft Identity SDK will automatically both share credentials across your applications and invoke hello broker if it's present on their device.</span></span>

