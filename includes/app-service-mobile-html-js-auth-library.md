### <a name="server-auth"></a>Procédure : authentification auprès d’un fournisseur (flux serveur)
les applications mobiles toohave gérer les processus d’authentification hello dans votre application, vous devez inscrire votre application avec votre fournisseur d’identité. Dans votre Service d’applications Azure, vous devez tooconfigure ID de l’application hello et secret fournie par votre fournisseur.
Pour plus d’informations, consultez le didacticiel de hello [ajouter l’authentification tooyour application](../articles/app-service-mobile/app-service-mobile-cordova-get-started-users.md).

Une fois que vous avez enregistré votre fournisseur d’identité, appelez hello `.login()` méthode avec le nom hello de votre fournisseur. Par exemple, toologin avec Facebook utiliser hello suivant de code :

```
client.login("facebook").done(function (results) {
     alert("You are now logged in as: " + results.userId);
}, function (err) {
     alert("Error: " + err);
});
```

les valeurs valides Hello pour le fournisseur de hello sont 'aad', 'facebook', 'google', 'microsoftaccount' et « twitter ».

> [!NOTE]
> L’authentification Google ne fonctionne pour le moment pas via le flux serveur.  tooauthenticate avec Google, vous devez utiliser un [méthode de flux client](#client-auth).

Dans ce cas, du Service d’applications Azure gère les flux d’authentification hello OAuth 2.0.  Il affiche la page de connexion hello du fournisseur sélectionné de hello et génère un jeton d’authentification du Service d’applications après l’ouverture de session réussie avec le fournisseur d’identité hello. fonction de connexion Hello, lorsque vous avez terminé, retourne un objet JSON qui expose hello ID d’utilisateur et le Service application jeton d’authentification dans les champs de nom d’utilisateur et authenticationToken hello, respectivement. Ce jeton peut être mis en cache et réutilisé jusqu'à ce qu'il arrive à expiration.

###<a name="client-auth"></a>Procédure : authentification auprès d’un fournisseur (flux client)

Votre application peut également indépendamment contactez le fournisseur d’identité hello, puis saisissez hello retourné tooyour jeton du Service d’applications pour l’authentification. Ce flux du client vous permet de tooprovide une expérience d’authentification unique pour les utilisateurs ou les données d’utilisateur supplémentaires tooretrieve hello fournisseur d’identité.

#### <a name="social-authentication-basic-example"></a>Exemple de base de l’authentification sociale

Cet exemple utilise le SDK client Facebook pour l'authentification :

```
client.login(
     "facebook",
     {"access_token": token})
.done(function (results) {
     alert("You are now logged in as: " + results.userId);
}, function (err) {
     alert("Error: " + err);
});

```
Cet exemple suppose que ce jeton hello fournies par le fournisseur de respectifs hello SDK est stocké dans la variable de jeton hello.

#### <a name="microsoft-account-example"></a>Exemple de compte Microsoft

Hello suivant montre comment utiliser hello Live SDK, qui prend en charge authentification unique pour les applications du Windows Store à l’aide de Microsoft Account :

```
WL.login({ scope: "wl.basic"}).then(function (result) {
      client.login(
            "microsoftaccount",
            {"authenticationToken": result.session.authentication_token})
      .done(function(results){
            alert("You are now logged in as: " + results.userId);
      },
      function(error){
            alert("Error: " + err);
      });
});

```

Cet exemple obtient un jeton de Live Connect, qui est fourni tooyour du Service d’applications en appelant la fonction de connexion hello.

###<a name="auth-getinfo"></a>Comment : obtenir des informations sur l’utilisateur de hello authentifié

informations d’authentification Hello peuvent être récupérées à partir de hello `/.auth/me` appeler de point de terminaison à l’aide de HTTP avec n’importe quelle bibliothèque AJAX.  Veillez à définir hello `X-ZUMO-AUTH` jeton d’authentification tooyour en-tête.  jeton d’authentification Hello est stocké dans `client.currentUser.mobileServiceAuthenticationToken`.  Par exemple, toouse hello fetch API :

```
var url = client.applicationUrl + '/.auth/me';
var headers = new Headers();
headers.append('X-ZUMO-AUTH', client.currentUser.mobileServiceAuthenticationToken);
fetch(url, { headers: headers })
    .then(function (data) {
        return data.json()
    }).then(function (user) {
        // hello user object contains hello claims for hello authenticated user
    });
```

L’extraction est disponible sous forme de [package npm](https://www.npmjs.com/package/whatwg-fetch) ou de téléchargement par navigateur à partir de [CDNJS](https://cdnjs.com/libraries/fetch). Vous pouvez également utiliser jQuery ou informations hello de toofetch une autre API AJAX.  Les données sont reçues sous la forme d’un objet JSON.
