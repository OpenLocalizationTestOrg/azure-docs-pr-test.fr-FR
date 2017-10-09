
Hello l’exemple précédent a montré une standard sign-in, ce qui nécessite hello client toocontact deux hello identité fournisseur et hello Azure service principal chaque démarrage d’application hello. Cette méthode est inefficace, et vous pouvez avoir des problèmes liés à l’utilisation si de nombreux clients essaient de toostart votre application simultanément. Une meilleure approche est le jeton d’autorisation toocache hello retournées par hello service Azure et try toouse cela tout d’abord avant d’utiliser un fournisseur connectez-vous.

> [!NOTE]
> Vous pouvez mettre en cache jeton hello émis par hello principaux services Azure, quelle que soit la que vous utilisez l’authentification de client géré ou par le service. Ce didacticiel utilise cette dernière.
>
>

1. Ouvrir le fichier de ToDoActivity.java hello et ajouter hello suivant les instructions d’importation :

        import android.content.Context;
        import android.content.SharedPreferences;
        import android.content.SharedPreferences.Editor;
2. Ajouter hello suivant membres toohello `ToDoActivity` classe.

        public static final String SHAREDPREFFILE = "temp";    
        public static final String USERIDPREF = "uid";    
        public static final String TOKENPREF = "tkn";    
3. Dans le fichier de ToDoActivity.java hello, ajouter hello définition pourquoi `cacheUserToken` (méthode).

        private void cacheUserToken(MobileServiceUser user)
        {
            SharedPreferences prefs = getSharedPreferences(SHAREDPREFFILE, Context.MODE_PRIVATE);
            Editor editor = prefs.edit();
            editor.putString(USERIDPREF, user.getUserId());
            editor.putString(TOKENPREF, user.getAuthenticationToken());
            editor.commit();
        }    

    Cette méthode stocke hello ID d’utilisateur et le jeton dans un fichier de préférence qui est marqué comme privé. Cela doit protéger accès toohello cache afin que les autres applications sur l’appareil de hello n’ont pas de jeton d’accès toohello. préférence de Hello est sandbox pour l’application hello. Toutefois, si quelqu'un a dispositif toohello d’accès, il est possible peut bénéficier des accès cache de jeton toohello par d’autres moyens.

   > [!NOTE]
   > Vous pouvez renforcer la protection jeton hello avec le chiffrement, si les données tooyour de jeton d’accès sont considéré comme hautement confidentielles et un utilisateur peut vous faire gagner DISPOSITIF toohello d’accès. Une solution entièrement sécurisée est abordée dans ce didacticiel, hello et dépend de vos exigences de sécurité.
   >
   >
4. Dans le fichier de ToDoActivity.java hello, ajouter hello définition pourquoi `loadUserTokenCache` (méthode).

        private boolean loadUserTokenCache(MobileServiceClient client)
        {
            SharedPreferences prefs = getSharedPreferences(SHAREDPREFFILE, Context.MODE_PRIVATE);
            String userId = prefs.getString(USERIDPREF, null);
            if (userId == null)
                return false;
            String token = prefs.getString(TOKENPREF, null);
            if (token == null)
                return false;

            MobileServiceUser user = new MobileServiceUser(userId);
            user.setAuthenticationToken(token);
            client.setCurrentUser(user);

            return true;
        }
5. Bonjour *ToDoActivity.java* de fichiers, remplacez hello `authenticate` méthode avec hello suivant de méthode, qui utilise un cache de jeton. Modifier le fournisseur de connexion hello si vous voulez toouse un compte autre que Google.

        private void authenticate() {
            // We first try tooload a token cache if one exists.
            if (loadUserTokenCache(mClient))
            {
                createTable();
            }
            // If we failed tooload a token cache, login and create a token cache
            else
            {
                // Login using hello Google provider.    
                ListenableFuture<MobileServiceUser> mLogin = mClient.login(MobileServiceAuthenticationProvider.Google);

                Futures.addCallback(mLogin, new FutureCallback<MobileServiceUser>() {
                    @Override
                    public void onFailure(Throwable exc) {
                        createAndShowDialog("You must log in. Login Required", "Error");
                    }           
                    @Override
                    public void onSuccess(MobileServiceUser user) {
                        createAndShowDialog(String.format(
                                "You are now logged in - %1$2s",
                                user.getUserId()), "Success");
                        cacheUserToken(mClient.getCurrentUser());
                        createTable();    
                    }
                });
            }
        }
6. Générez hello application et tester l’authentification à l’aide d’un compte valide. Exécutez ceci au moins deux fois. Pendant hello exécutez d’abord, vous devez recevoir une invite de commandes toosign dans et créer le cache de jeton hello. Après cela, chaque série de tentatives tooload hello cache de jetons pour l’authentification. Vous ne devez pas être toosign requis dans.
