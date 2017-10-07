---
title: "kit de développement logiciel aaaMFA pour les applications personnalisées | Documents Microsoft"
description: "Cet article vous explique comment toodownload et utilisez hello vérification d’en deux étapes tooenable SDK Azure MFA pour vos applications personnalisées."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 1c152f67-be02-42a5-a0c7-246fb6b34377
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/03/2017
ms.author: kgremban
ms.openlocfilehash: 10e02e844bf3928575bfca79dbc34717a31a08b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="building-multi-factor-authentication-into-custom-apps-sdk"></a>Création de Multi-Factor Authentication dans des applications personnalisées (SDK)

Hello Kit de développement logiciel (SDK) Azure multi-Factor Authentication vous permet de dans que créer vérification en deux étapes directement hello connexion ou transaction traite des applications dans votre locataire Azure AD.

Hello SDK multi-Factor Authentication est disponible pour c#, Visual Basic (.NET), Java, Perl, PHP et Ruby. Hello SDK fournit un wrapper mince entourant la vérification en deux étapes. Il inclut tous les éléments que nécessaires toowrite votre code, y compris les fichiers de code source commentés, exemples de fichiers et un fichier Lisez-moi détaillé. Chaque SDK inclut également un certificat et la clé privée pour chiffrer les transactions qui sont unique tooyour fournisseur d’authentification multifacteur. Tant que vous disposez d’un fournisseur, vous pouvez télécharger hello SDK dans toutes les langues et formats dont vous avez besoin.

structure de Hello Hello API Bonjour SDK multi-Factor Authentication est simple. Rendre une fonction unique d’appeler l’API tooan avec les paramètres d’option multifacteur hello (par exemple, le mode de vérification) et les données utilisateur (comme toocall numéro de téléphone hello ou toovalidate numéro de code confidentiel hello). appel de fonction hello dans toohello de demandes de services web traduire Hello API Service nuage Azure multi-Factor Authentication. Tous les appels doivent inclure un certificat privé de toohello référence qui est inclus dans chaque SDK.

Car hello API n’ont pas toousers accès inscrit dans Azure Active Directory, vous devez fournir les informations utilisateur dans un fichier ou d’une base de données. En outre, hello API ne fournissent pas d’inscription ou l’utilisateur les fonctionnalités de gestion, par conséquent, vous devez toobuild ces processus dans votre application.

> [!IMPORTANT]
> toodownload hello du Kit de développement logiciel, vous devez toocreate un fournisseur de d’authentification multifacteur Azure, même si vous disposez de licences Azure MFA, AAD Premium ou EMS. Si vous créez un fournisseur d’authentification d’Azure multi-Factor à cet effet et que vous avez déjà des licences, assurez-vous que toocreate hello fournisseur avec hello **par utilisateur activé** modèle. Ensuite, liez hello fournisseur toohello répertoire qui contient les licences Azure MFA, Azure AD Premium ou EMS hello. Cette configuration garantit que vous êtes facturé uniquement si vous avez plusieurs utilisateurs uniques à l’aide de hello SDK que nombre hello de licences que vous possédez.


## <a name="download-hello-sdk"></a>Télécharger hello SDK
Téléchargement hello SDK Azure multi-Factor nécessite un [fournisseur d’authentification multifacteur Azure](multi-factor-authentication-get-started-auth-provider.md).  Cela requiert un abonnement Azure complet, même si vous possédez des licences Azure MFA, Azure AD Premium ou Enterprise Mobility Suite.  hello de toodownload SDK, accédez toohello portail de gestion multi-Factor. Vous pouvez atteindre portal de hello en gérant hello du fournisseur multi-Factor Authentication directement, ou en cliquant sur hello **« Portail de toohello Go »** lien dans la page de paramètres de service de l’authentification Multifacteur hello.

### <a name="download-from-hello-azure-classic-portal"></a>Télécharger à partir de hello portail Azure classic
1. Connectez-vous à toohello [portail Azure classic](https://manage.windowsazure.com) en tant qu’administrateur.
2. Sur hello gauche, sélectionnez **Active Directory**.
3. Page Active Directory hello, à sélectionner supérieur de hello **fournisseurs d’authentification multifacteur**
4. Au bas de hello sélectionnez **gérer**. Une nouvelle page s’ouvre.
5. Dans hello sur la gauche, en bas de hello, cliquez sur **SDK**.
   <center>![Télécharger](./media/multi-factor-authentication-sdk/download.png)</center>
6. Sélectionnez le langage hello et cliquez sur un liens de téléchargement de hello.
7. Enregistrer le fichier téléchargé hello.

### <a name="download-from-hello-service-settings"></a>Télécharger à partir des paramètres de service hello
1. Connectez-vous à toohello [portail Azure classic](https://manage.windowsazure.com) en tant qu’administrateur.
2. Sur hello gauche, sélectionnez **Active Directory**.
3. Double-cliquez sur votre instance d’Azure AD.
4. Cliquez sur supérieur de hello **configurer**
5. Sous Authentification multifacteur, sélectionnez **Gérer les paramètres du service**
   ![Télécharger](./media/multi-factor-authentication-sdk/download2.png)
6. Dans la page Paramètres de services hello, bas hello écran hello, cliquez sur **Go toohello portal**. Une nouvelle page s’ouvre.
   ![Télécharger](./media/multi-factor-authentication-sdk/download3a.png)
7. Dans hello sur la gauche, en bas de hello, cliquez sur **SDK**.
8. Sélectionnez le langage hello et cliquez sur un liens de téléchargement de hello.
9. Enregistrer le fichier téléchargé hello.

## <a name="whats-in-hello-sdk"></a>Nouveautés dans hello SDK
Hello SDK inclut hello éléments suivants :

* **LISEZ-MOI**. Explique comment toouse hello API d’authentification multifacteur dans une application nouvelle ou existante.
* **Fichiers source** pour l'authentification multifacteur
* **Certificat client** que vous utilisez toocommunicate avec hello service d’authentification multifacteur
* **Clé privée** pour le certificat de hello
* **Résultats des appels** Une liste des codes de résultats d’appels. tooopen ce fichier, utilisez une application avec mise en forme, telle que WordPad. Hello d’utilisation appeler tootest de codes de résultat et résoudre les problèmes de mise en œuvre de hello de l’authentification multifacteur dans votre application. Ce ne sont pas des codes d'état de l'authentification.
* **Exemples.** Exemple de code pour une implémentation fonctionnelle de base de l'authentification multifacteur.

> [!WARNING]
> certificat de client Hello est un certificat privé unique qui a été généré spécialement pour vous. Ne partagez pas ou n’égarez pas ce fichier. Il s’agit de sécurité de vos communications avec le service d’authentification multifacteur hello hello tooensuring clé.

## <a name="code-sample"></a>Exemple de code
Cet exemple de code montre comment toouse hello API Bonjour voix de mode standard SDK Azure multi-Factor Authentication tooadd appeler application tooyour de vérification. Mode standard est un appel téléphonique auquel hello tooby répond d’utilisateur en appuyant sur la touche # de hello.

Cet exemple utilise hello c# .NET 2.0 SDK multi-Factor Authentication dans une application ASP.NET de base avec une logique côté serveur c#, mais les processus hello sont similaire dans d’autres langages. Car hello SDK inclut des fichiers sources, non des fichiers exécutables, vous pouvez générer des fichiers de hello et y fait référence ou les inclure directement dans votre application.

> [!NOTE]
> Quand vous implémentez l’authentification multifacteur, utiliser des méthodes supplémentaires hello (appel téléphonique ou SMS) en tant que vérification secondaire ou tertiaire toosupplement votre méthode d’authentification principale (nom d’utilisateur et mot de passe). Ces méthodes ne sont pas conçues comme des méthodes d’authentification principale.

### <a name="code-sample-overview"></a>Vue d'ensemble d’un exemple de code
Cet exemple de code pour une application de démonstration web simple utilise un appel téléphonique avec un # réponse de la clé tooverify hello authentification de l’utilisateur. Ce facteur d'appel téléphonique est appelé mode standard dans l'authentification multifacteur.

code côté client de Hello n’inclut pas tous les éléments spécifiques à l’authentification multifacteur. Étant donné que les facteurs d’authentification supplémentaires hello sont indépendantes de l’authentification principale de hello, vous pouvez les ajouter sans modifier l’interface de connexion existant hello. Hello API Bonjour SDK multi-Factor vous permettre de personnaliser l’expérience utilisateur hello, mais vous n’ayez pas toochange rien du tout.

code de Hello côté serveur ajoute l’authentification en mode standard à l’étape 2. Il crée un objet PfAuthParams avec les paramètres de hello qui sont requis pour la vérification en mode standard : nom d’utilisateur, nombre et le mode de téléphone et hello du chemin d’accès toohello certificat client (CertFilePath), qui est requis pour chaque appel. Pour une démonstration de tous les paramètres de PfAuthParams, voir fichier d’exemple hello Bonjour SDK.

Ensuite, le code de hello transmet hello PfAuthParams objet toohello pf_authenticate() une fonction. valeur de retour Hello indique la réussite de hello ou l’échec d’authentification de hello. Bonjour des paramètres, callStatus et un code d’erreur, contiennent des informations de résultat d’appel supplémentaire. codes de résultat d’appel Hello sont documentées dans le fichier de résultats d’appel hello Bonjour SDK.

Cette implémentation minimale peut être écrite en quelques lignes. Toutefois, dans le code de production, vous pouvez inclure une gestion plus sophistiquée des erreurs, un autre code de base de données et une expérience utilisateur améliorée.

### <a name="web-client-code"></a>Code du client Web
Hello Voici code du client web pour une page de démonstration.

    <%@ Page Language="C#" AutoEventWireup="true" CodeFile="Default.aspx.cs" Inherits="\_Default" %>

    <!DOCTYPE html>

    <html xmlns="http://www.w3.org/1999/xhtml">
    <head runat="server">
    <title>Multi-Factor Authentication Demo</title>
    </head>
    <body>
    <h1>Azure Multi-Factor Authentication Demo</h1>
    <form id="form1" runat="server">

    <div style="width:auto; float:left">
    Username:&nbsp;<br />
    Password:&nbsp;<br />
    </div>

    <div">
    <asp:TextBox id="username" runat="server" width="100px"/><br />
    <asp:Textbox id="password" runat="server" width="100px" TextMode="password" /><br />
    </div>

    <asp:Button id="btnSubmit" runat="server" Text="Log in" onClick="btnSubmit_Click"/>

    <p><asp:Label ID="lblResult" runat="server"></asp:Label></p>

    </form>
    </body>
    </html>


### <a name="server-side-code"></a>Code côté serveur
Bonjour suivant le code côté serveur, l’authentification multifacteur est configurée et exécutée à l’étape 2. Mode standard (MODE_STANDARD) est qu'un utilisateur de hello toowhich appel téléphonique répond en appuyant sur la touche # de hello.

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Web;
    using System.Web.UI;
    using System.Web.UI.WebControls;

    public partial class \_Default : System.Web.UI.Page
    {
        protected void Page_Load(object sender, EventArgs e)
        {
        }

        protected void btnSubmit_Click(object sender, EventArgs e)
        {
            // Step 1: Validate hello username and password
            if (username.Text != "Contoso" || password.Text != "password")
            {
                lblResult.ForeColor = System.Drawing.Color.Red;
                lblResult.Text = "Username or password incorrect.";
            }
            else
            {
                // Step 2: Perform multi-factor authentication

                // Add call details from hello user database.
                PfAuthParams pfAuthParams = new PfAuthParams();
                pfAuthParams.Username = username.Text;
                pfAuthParams.Phone = "5555555555";
                pfAuthParams.Mode = pf_auth.MODE_STANDARD;

                // Specify a client certificate
                // NOTE: This file contains hello private key for hello client
                // certificate. It must be stored with appropriate file
                // permissions.
                pfAuthParams.CertFilePath = "c:\\cert_key.p12";

                // Perform phone-based authentication
                int callStatus;
                int errorId;

                if(pf_auth.pf_authenticate(pfAuthParams, out callStatus, out errorId))
                {
                    lblResult.ForeColor = System.Drawing.Color.Green;
                    lblResult.Text = "Multi-Factor Authentication succeeded.";
                }
                else
                {
                    lblResult.ForeColor = System.Drawing.Color.Red;
                    lblResult.Text = "Multi-Factor Authentication failed.";
                }
            }

        }
    }
