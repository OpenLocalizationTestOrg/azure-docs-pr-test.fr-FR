---
title: "Personnalisation de l’interface utilisateur (IU) - Azure AD B2C | Documents Microsoft"
description: "Une rubrique sur les fonctionnalités de personnalisation d’interface utilisateur hello utilisateur dans Azure Active Directory B2C"
services: active-directory-b2c
documentationcenter: 
author: saeedakhter-msft
manager: krassk
editor: parakhj
ms.assetid: 99f5a391-5328-471d-a15c-a2fafafe233d
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/16/2017
ms.author: saeedakhter-msft
ms.openlocfilehash: 04f8c5f1277f8d4409cd10971d22a0ebd2024785
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-customize-hello-azure-ad-b2c-user-interface-ui"></a>Azure B2C Active Directory : Personnaliser hello Azure AD B2C interface utilisateur)

L’expérience utilisateur est primordiale dans une application orientée client.  Développez votre clientèle en créant des expériences utilisateur avec hello apparence de votre image de marque. Azure Active Directory B2C (Azure AD B2C) vous permet de personnaliser les pages d’inscription, de connexion, de modification du profil et de réinitialisation du mot de passe avec le contrôle pixel-perfect.

> [!NOTE]
> fonctionnalité de personnalisation UI page Hello décrite dans cet article ne s’applique pas toohello signe dans une seule stratégie, sa page de réinitialisation de mot de passe qui l’accompagne et des messages électroniques de vérification.  Ces fonctionnalités utilisent hello [fonctionnalité de marque de société](../active-directory/active-directory-add-company-branding.md) à la place.
>

Cet article traite des rubriques suivantes de hello :

* fonctionnalité de personnalisation de l’interface utilisateur de page de Hello.
* Outil de téléchargement HTML contenu tooAzure stockage d’objets Blob pour une utilisation avec la fonctionnalité de personnalisation de l’interface utilisateur de page hello.
* éléments d’interface utilisateur Hello utilisés par Azure AD B2C que vous pouvez personnaliser à l’aide de feuilles de Style en cascade (CSS).
* Meilleures pratiques lors de l’exercice de cette fonctionnalité.

## <a name="hello-page-ui-customization-feature"></a>fonctionnalité de personnalisation de l’interface utilisateur de page Hello

Vous pouvez personnaliser hello apparence de mot de passe client d’abonnement, connectez-vous, réinitialisation et modification de profils de pages (en configurant [stratégies](active-directory-b2c-reference-policies.md)). Vos clients bénéficieront d’une expérience transparente lors de la navigation entre votre application et les pages fournies par Azure AD B2C.

Contrairement à d’autres services, où les options de l’interface utilisateur, Azure AD B2C utilise un simple et moderne approchent tooUI personnalisation.

Voici comment cela fonctionne : Azure AD B2C exécute le code dans le navigateur client et utilise une approche moderne appelée [partage des ressources cross-origin (CORS)](http://www.w3.org/TR/cors/).  Au moment de l’exécution, le contenu est chargé depuis une URL que vous spécifiez dans une stratégie. Vous pouvez spécifier des URL différentes pour différentes pages. Une fois le contenu chargé à partir de votre URL est fusionné avec un fragment HTML inséré à partir d’Azure AD B2C, page de hello est affichée tooyour client. Il vous suffit de toodo est :

1. Créer du contenu avec vide HTML5 correct `<div id="api"></div>` élément trouve quelque part dans hello `<body>`. Marques de cet élément où hello Azure AD B2C contenu est inséré.
1. Héberger votre contenu sur un point de terminaison HTTPS (avec CORS activé). Notez que vous devez activer à la fois les méthodes de demande GET et OPTIONS lors de la configuration de CORS.
1. Utilisez CSS toostyle hello éléments d’interface utilisateur Azure AD B2C insère.

### <a name="a-basic-example-of-customized-html"></a>Un exemple de base de code HTML personnalisé

Bonjour à l’exemple suivant est le contenu HTML plus simple de hello, que vous pouvez utiliser tootest cette fonctionnalité. Hello d’utilisation [outil d’assistance](active-directory-b2c-reference-ui-customization-helper-tool.md) tooupload et configurer ce contenu sur votre stockage d’objets Blob Azure. Vous pouvez ensuite vérifier que les boutons de base, non stylisé hello et champs de formulaire sur chaque page sont affichés et fonctionnelles.

```HTML
<!DOCTYPE html>
<html>
    <head>
        <title>!Add your title here!</title>
    </head>
    <body>
        <div id="api"></div>   <!-- Leave this element empty because Azure AD B2C will insert content here. -->
    </body>
</html>
```

## <a name="test-out-hello-ui-customization-feature"></a>Tester la fonctionnalité de personnalisation de l’interface utilisateur de hello

Vous souhaitez tootry fonctionnalité de personnalisation de l’interface utilisateur hello à l’aide de notre exemple de code HTML et CSS contenu ?  Nous vous avons fourni [un outil d’assistance](active-directory-b2c-reference-ui-customization-helper-tool.md) qui télécharge et configure notre exemple de contenu sur votre stockage Azure Blob.

> [!NOTE]
> Vous pouvez héberger le contenu de votre interface utilisateur sur tous types d’emplacements : serveurs web, CDN, AWS S3, systèmes de partage de fichiers, etc. Tant que le contenu hello est hébergé sur un point de terminaison HTTPS disponible publiquement avec CORS activé, vous êtes bon toogo. Nous utilisons Azure Blob Storage à titre indicatif uniquement.
>

## <a name="hello-ui-fragments-embedded-by-azure-ad-b2c"></a>fragments de l’interface utilisateur Hello incorporés par Azure AD B2C

Hello sections suivantes répertorient les fragments de hello HTML5 Azure AD B2C fusionne hello `<div id="api"></div>` élément se trouve dans votre contenu. **N’insérez pas ces fragments dans votre contenu HTML5.** Bonjour Azure AD B2C service les insère au moment de l’exécution. Utilisez ces fragments en tant que référence lors de la conception de vos propres feuilles de Style en cascade (CSS).

### <a name="fragment-inserted-into-hello-identity-provider-selection-page"></a>Fragment inséré hello « Page Sélection du fournisseur d’identité »

Cette page contient une liste d’identité, les fournisseurs qui hello utilisateur peuvent choisir de pendant l’inscription ou de la connexion. Ces boutons incluent des fournisseurs d’identité sociale tels que Facebook et Google+ ou de comptes locaux (basés sur une adresse e-mail ou un nom d’utilisateur).

```HTML
<div id="api" data-name="IdpSelections">
    <div class="intro">
         <p>Sign up</p>
    </div>

    <div>
        <ul>
            <li>
                <button class="accountButton" id="FacebookExchange">Facebook</button>
            </li>
            <li>
                <button class="accountButton" id="GoogleExchange">Google+</button>
            </li>
            <li>
                <button class="accountButton" id="SignUpWithLogonEmailExchange">Email</button>
            </li>
        </ul>
    </div>
</div>
```

### <a name="fragment-inserted-into-hello-local-account-sign-up-page"></a>Fragment inséré hello « page d’inscription du compte Local »

Cette page contient un formulaire d’inscription du compte local basée sur une adresse e-mail ou un nom d’utilisateur. formulaire de Hello peut contenir différents contrôles d’entrée tels que la zone de texte, zone de saisie de mot de passe, case d’option, zones de liste déroulante de sélection unique et sélections plusieurs cases à cocher.

```HTML
<div id="api" data-name="SelfAsserted">
    <div class="intro">
        <p>Create your account by providing hello following details</p>
    </div>

    <div id="attributeVerification">
        <div class="errorText" id="passwordEntryMismatch" style="display: none;">hello password entry fields do not match. Please enter hello same password in both fields and try again.</div>
        <div class="errorText" id="requiredFieldMissing" style="display: none;">A required field is missing. Please fill out all required fields and try again.</div>
        <div class="errorText" id="fieldIncorrect" style="display: none;">One or more fields are filled out incorrectly. Please check your entries and try again.</div>
        <div class="errorText" id="claimVerificationServerError" style="display: none;"></div>
        <div class="attr" id="attributeList">
            <ul>
                <li>
                    <div class="attrEntry validate">
                        <div>
                            <div class="verificationInfoText" id="email_intro" style="display: inline;">Verification is necessary. Please click Send button.</div>
                            <div class="verificationInfoText" id="email_info" style="display:none">Verification code has been sent tooyour inbox. Please copy it toohello input box below.</div>
                            <div class="verificationSuccessText" id="email_success" style="display:none">E-mail address verified. You can now continue.</div>
                            <div class="verificationErrorText" id="email_fail_retry" style="display:none">Incorrect code, try again.</div>
                            <div class="verificationErrorText" id="email_fail_no_retry" style="display:none">Exceeded number of retries you need toosend new code.</div>
                            <div class="verificationErrorText" id="email_fail_server" style="display:none">Server error, please try again</div>
                            <div class="verificationErrorText" id="email_incorrect_format" style="display:none">Incorect format.</div>
                        </div>

                    <div class="helpText show">This information is required</div>
                        <label>Email</label>
                        <input id="email" class="textInput" type="text" placeholder="Email" required="" autofocus=""><a href="javascript:void(0)" onclick="selfAssertedClient.showHelp('Email address that can be used toocontact you.');" class="tiny">What is this?</a>

                    <div class="buttons verify" claim_id="email">
                        <div id="email_ver_wait" class="working" style="display: none;"></div>
                            <label id="email_ver_input_label" for="email_ver_input" style="display: none;">Verification code</label>
                            <input id="email_ver_input" type="text" placeholder="Verification code" style="display:none">
                            <button id="email_ver_but_send" class="sendButton" type="button" style="display: inline;">Send verification code</button>
                            <button id="email_ver_but_verify" class="verifyButton" type="button" style="display:none">Verify code</button>
                            <button id="email_ver_but_resend" class="sendButton" type="button" style="display:none">Send new code</button>
                            <button id="email_ver_but_edit" class="editButton" type="button" style="display:none">Change e-mail</button>
                            <button id="email_ver_but_default" class="defaultButton" type="button" style="display:none">Default</button>
                        </div>
                    </div>
                </li>
                <li>
                    <div class="attrEntry">
                        <div class="helpText">8-16 characters, containing 3 out of 4 of hello following: Lowercase characters, uppercase characters, digits (0-9), and one or more of hello following symbols: @ # $ % ^ &amp; * - _ + = [ ] { } | \ : ' , ? / ` ~ " ( ) ; .This information is required</div>
                        <label>Enter password</label>
                        <input id="password" class="textInput" type="password" placeholder="Enter password" pattern="^((?=.*[a-z])(?=.*[A-Z])(?=.*\d)|(?=.*[a-z])(?=.*[A-Z])(?=.*[^A-Za-z0-9])|(?=.*[a-z])(?=.*\d)(?=.*[^A-Za-z0-9])|(?=.*[A-Z])(?=.*\d)(?=.*[^A-Za-z0-9]))([A-Za-z\d@#$%^&amp;*\-_+=[\]{}|\\:',?/`~&quot;();!]|\.(?!@)){8,16}$" title="8-16 characters, containing 3 out of 4 of hello following: Lowercase characters, uppercase characters, digits (0-9), and one or more of hello following symbols: @ # $ % ^ &amp; * - _ + = [ ] { } | \ : ' , ? / ` ~ &quot; ( ) ; ." required=""><a href="javascript:void(0)" onclick="selfAssertedClient.showHelp('Enter password');" class="tiny">What is this?</a>
                    </div>
                </li>
                <li>
                    <div class="attrEntry">
                        <div class="helpText"> This information is required</div>
                        <label>Reenter password</label>
                        <input id="reenterPassword" class="textInput" type="password" placeholder="Reenter password" pattern="^((?=.*[a-z])(?=.*[A-Z])(?=.*\d)|(?=.*[a-z])(?=.*[A-Z])(?=.*[^A-Za-z0-9])|(?=.*[a-z])(?=.*\d)(?=.*[^A-Za-z0-9])|(?=.*[A-Z])(?=.*\d)(?=.*[^A-Za-z0-9]))([A-Za-z\d@#$%^&amp;*\-_+=[\]{}|\\:',?/`~&quot;();!]|\.(?!@)){8,16}$" title=" " required=""><a href="javascript:void(0)" onclick="selfAssertedClient.showHelp('Reenter password');" class="tiny">What is this?</a>
                    </div>
                </li>
                <li>
                    <div class="attrEntry">
                        <div class="helpText">This information is required</div>
                        <label>Name</label>
                        <input id="displayName" class="textInput" type="text" placeholder="Name" required=""><a href="javascript:void(0)" onclick="selfAssertedClient.showHelp('Your display name.');" class="tiny">What is this?</a>
                    </div>
                </li>
                <li>
                    <div class="attrEntry">
                        <div class="helpText"></div>
                        <label>Gender</label>
                        <input id="extension_Gender_F" name="extension_Gender" type="radio" value="F" autofocus="">
                        <label for="extension_Gender_F">Female</label>
                        <input id="extension_Gender_M" name="extension_Gender" type="radio" value="M">
                        <label for="extension_Gender_M">Male</label>
                        <a href="javascript:void(0)" onclick="selfAssertedClient.showHelp('');" class="tiny">What is this?</a>
                    </div>
                </li>
                <li>
                    <div class="attrEntry">
                        <div class="helpText"></div>
                        <label>Loyalty number</label>
                        <input id="extension_MemNum" class="textInput" type="text" placeholder="Loyalty number"><a href="javascript:void(0)" onclick="selfAssertedClient.showHelp('Membership number');" class="tiny">What is this?</a>
                    </div>
                </li>
                <li>
                    <div class="attrEntry">
                        <div class="helpText"></div>
                        <label>State</label>
                        <select class="dropdown_single" id="state">
                            <option style="display:none" disabled="disabled" value="placeholder" selected="">State</option>
                            <option value="WA">Washington</option>
                            <option value="NY">New York</option>
                            <option value="CA">California</option>
                        </select>
                        <a href="javascript:void(0)" onclick="selfAssertedClient.showHelp('Your residential state or province.');" class="tiny">What is this?</a>
                    </div>
                </li>
                <li>
                    <div class="attrEntry">
                        <div class="helpText">This information is required</div>
                        <label>Zip code</label>
                        <input id="postalCode" class="textInput" type="text" placeholder="Zip code" required=""><a href="javascript:void(0)" onclick="selfAssertedClient.showHelp('hello postal code of your address.');" class="tiny">What is this?</a>
                    </div>
                </li>
            </ul>
        </div>
        <div class="buttons"> <button id="continue" disabled="">Create</button> <button id="cancel">Cancel</button></div>
    </div>
    <div class="verifying-modal">
        <div class="preloader"> <img src="https://login.microsoftonline.com/static/img/win8loader.gif" alt="Please wait"></div>
        <div id="verifying_blurb"></div>
    </div>
</div>
```

### <a name="fragment-inserted-into-hello-social-account-sign-up-page"></a>Fragment inséré hello « « sociale account page d’inscription »

Cette page peut s’afficher lors de l’inscription à l’aide d’un compte existant depuis un fournisseur d’identité sociale tel que Facebook ou Google+.  Il est utilisé lorsque des informations supplémentaires doivent être collectées à partir de l’utilisateur final de hello à l’aide d’un formulaire d’inscription. Cette page est similaire toohello compte local d’abonnement (illustrée dans la section précédente de hello) à l’exception de hello des champs d’entrée de mot de passe hello.

### <a name="fragment-inserted-into-hello-unified-sign-up-or-sign-in-page"></a>Fragment inséré hello « Page d’inscription ou connectez-vous unifié »

Cette page gère l’inscription et la connexion des utilisateurs, qui peuvent utiliser les fournisseurs d’identité des réseaux sociaux, tels que Facebook ou Google+, ou des comptes locaux.

```HTML
<div id="api" data-name="Unified">
        <div class="social" role="form">
               <div class="intro">
                       <h2>Sign in with your social account</h2>
               </div>
               <div class="options">
                       <div><button class="accountButton firstButton" id="MicrosoftAccountExchange" tabindex="1">msa</button></div>
                       <div><button class="accountButton" id="FacebookExchange" tabindex="1">fb</button></div>
               </div>
        </div>
        <div class="divider">
               <h2>OR</h2>
        </div>
        <div class="localAccount" role="form">
               <div class="intro">
                       <h2>Sign in with your existing account</h2>
               </div>
               <div class="error pageLevel" aria-hidden="true" style="display: none;">
                       <p role="alert"></p>
               </div>
               <div class="entry">
                       <div class="entry-item">
                               <label for="logonIdentifier">Email Address</label> 
                               <div class="error itemLevel" aria-hidden="true" style="display: none;">
                                      <p role="alert"></p>
                               </div>
                               <input type="email" id="logonIdentifier" name="LogonIdentifier" pattern="^[a-zA-Z0-9.!#$%&amp;’*+/=?^_`{|}~-]+@[a-zA-Z0-9-]+(?:\.[a-zA-Z0-9-]+)*$" placeholder="LogonIdentifier" value="" tabindex="1">
                       </div>
                       <div class="entry-item">
                               <div class="password-label"> <label for="password">Password</label><a id="forgotPassword" tabindex="2">Forgot your password?</a></div>
                               <div class="error itemLevel" aria-hidden="true" style="display: none;">
                                      <p role="alert"></p>
                               </div>
                               <input type="password" id="password" name="Password" placeholder="Password" tabindex="1">
                       </div>
                       <div class="working"></div>
                       <div class="buttons"> <button id="next" tabindex="1">Sign in</button> </div>
               </div>
               <div class="divider">
                       <h2>OR</h2>
               </div>
               <div class="create">
                       <p>Don't have an account?<a id="createAccount" tabindex="1">Sign up now</a> </p>
               </div>
        </div>
</div>
```

### <a name="fragment-inserted-into-hello-multi-factor-authentication-page"></a>Fragment inséré hello « page multi-Factor authentication »

Cette page permet aux utilisateurs de vérifier leurs numéros de téléphone (par voie textuelle ou vocale) au cours de l’inscription ou de la connexion.

```HTML
<div id="api" data-name="Phonefactor">
    <div id="phonefactor_initial">
        <div class="intro">
            <p>Enter a number below that we can send a code via SMS or phone tooauthenticate you.</p>
        </div>
        <div class="errorText" id="errorMessage" style="display:none"></div>
        <div class="phoneEntry" id="phoneEntry">
            <div class="phoneNumber">
                <select id="countryCode" style="display:inline-block">
                    <option value="+93">Afghanistan (+93)</option>
                    <!-- Not all country codes listed -->
                    <option value="+44">United Kingdom (+44)</option>
                    <option value="+1" selected="">United States (+1)</option>
                    <!-- Not all country codes listed -->
                </select>
            </div>
            <div class="phoneNumber">
                <input type="text" id="localNumber" style="display:inline-block" placeholder="Phone number">
            </div>
        </div>
        <div id="codeVerification" style="display:none">
            <div>
                <p>Enter your verification code below, or <button id="retryCode" class="textButton">send a new code</button></p>
                <input type="text" id="verificationCode" placeholder="Verification code">
            </div>
        </div>
        <div class="buttons">
            <button id="verifyCode" class="sendInitialCodeButton">Send Code</button>
            <button id="verifyPhone" style="display:inline-block">Call Me</button>
            <button id="cancel" style="display:inline-block">Cancel</button>
        </div>
    </div>
    <div class="dialing-modal">
        <div class="preloader"> <img src="https://login.microsoftonline.com/static/img/win8loader.gif" alt="Please wait"></div>
        <div id="dialing_blurb"></div><div id="dialing_number"></div>
    </div>
</div>
```

### <a name="fragment-inserted-into-hello-error-page"></a>Fragment inséré hello « Page d’erreur « »

```HTML
<div id="api" class="error-page-content" data-name="GlobalException">
    <h2>Sorry, but we're having trouble signing you in.</h2>
    <div class="error-page-help">We track these errors automatically, but if hello problem persists feel free toocontact us. In hello meantime, please try again.</div>
    <div class="error-page-messagedetails">Your administrator hasn't provided any contact details.</div>
    <div class="error-page-messagedetails">
        <div class="error-page-correlationid">Correlation ID:1c4f0397-c6e4-4afe-bf74-42f488f2f15f</div>
        <div>Timestamp:2015-09-14 23:22:35Z</div>
        <div class="error-page-detail">AADB2C90065: A B2C client-side error 'Access is denied.' has occurred requesting hello remote resource.</div>
    </div>
</div>
```

## <a name="localizing-your-html-content"></a>Localisation de votre contenu HTML

Vous pouvez localiser votre contenu HTML en activant [« Personnalisation de la langue »](active-directory-b2c-reference-language-customization.md).  L’activation de cette fonctionnalité permet d’Azure AD B2C tooforward connecter à Open ID paramètre hello, `ui-locales`, tooyour le point de terminaison.  Votre serveur de contenu peut utiliser ce paramètre tooprovide personnalisé des pages HTML qui sont spécifiques au langage.

## <a name="things-tooremember-when-building-your-own-content"></a>Éléments tooremember lors de la création de votre propre contenu.

Si vous envisagez de fonctionnalité de personnalisation de l’interface utilisateur de toouse hello page, passez en revue hello suivant les meilleures pratiques :

* Ne copier le contenu de valeur par défaut de B2C hello Azure AD et essayez toomodify il. Il est meilleure toobuild votre contenu HTML5 à partir de zéro et toouse contenu par défaut en tant que référence.
* Pour des raisons de sécurité, nous ne vous permettent pas tooinclude code JavaScript dans votre contenu. La plupart des éléments doit être disponible en dehors de la zone de hello. Dans le cas contraire, utilisez [User Voice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c) toorequest nouvelles fonctionnalités.
* Versions de navigateur prises en charge :
  * Internet Explorer 11, 10, Edge
  * Prise en charge limitée pour Internet Explorer 9, 8
  * Google Chrome 42.0 et ultérieur
  * Mozilla Firefox 38.0 et ultérieur
