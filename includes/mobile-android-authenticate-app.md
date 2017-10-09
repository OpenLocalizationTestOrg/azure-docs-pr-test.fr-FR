
1. Ouvrez le projet de hello dans Android Studio.

2. Dans **Explorateur de projets** dans Android Studio, ouvrez le fichier ToDoActivity.java de hello et ajouter hello suivant les instructions d’importation :

        import java.util.concurrent.ExecutionException;
        import java.util.concurrent.atomic.AtomicBoolean;

        import android.content.Context;
        import android.content.SharedPreferences;
        import android.content.SharedPreferences.Editor;

        import com.microsoft.windowsazure.mobileservices.authentication.MobileServiceAuthenticationProvider;
        import com.microsoft.windowsazure.mobileservices.authentication.MobileServiceUser;

3. Ajouter hello suivant de méthode toohello **ToDoActivity** classe :

        // You can choose any unique number here toodifferentiate auth providers from each other. Note this is hello same code at login() and onActivityResult().
        public static final int GOOGLE_LOGIN_REQUEST_CODE = 1;

        private void authenticate() {
            // Login using hello Google provider.
            mClient.login("Google", "{url_scheme_of_your_app}", GOOGLE_LOGIN_REQUEST_CODE);
        }

        @Override
        protected void onActivityResult(int requestCode, int resultCode, Intent data) {
            // When request completes
            if (resultCode == RESULT_OK) {
                // Check hello request code matches hello one we send in hello login request
                if (requestCode == GOOGLE_LOGIN_REQUEST_CODE) {
                    MobileServiceActivityResult result = mClient.onActivityResult(data);
                    if (result.isLoggedIn()) {
                        // login succeeded
                        createAndShowDialog(String.format("You are now logged in - %1$2s", mClient.getCurrentUser().getUserId()), "Success");
                        createTable();
                    } else {
                        // login failed, check hello error message
                        String errorMessage = result.getErrorMessage();
                        createAndShowDialog(errorMessage, "Error");
                    }
                }
            }
        }

    Ce code crée un Bonjour de toohandle méthode processus d’authentification Google. Une boîte de dialogue affiche hello des ID d’utilisateur de hello authentifié. Vous pouvez agir uniquement si l’authentification a réussi.

    > [!NOTE]
    > Si vous utilisez un fournisseur d’identité autre que Google, modifiez la valeur hello passé toohello **connexion** tooone méthode Hello valeurs suivantes : _MicrosoftAccount_, _Facebook_, _Twitter_, ou _windowsazureactivedirectory_.

4. Bonjour **onCreate** (méthode), ajouter hello après la ligne de code après le code hello qui instancie hello `MobileServiceClient` objet.

        authenticate();

    Cet appel démarre le processus d’authentification hello.

5. Déplacer hello restant code après `authenticate();` Bonjour **onCreate** tooa méthode nouvelle **createTable** méthode :

        private void createTable() {

            // Get hello table instance toouse.
            mToDoTable = mClient.getTable(ToDoItem.class);

            mTextNewToDo = (EditText) findViewById(R.id.textNewToDo);

            // Create an adapter toobind hello items with hello view.
            mAdapter = new ToDoItemAdapter(this, R.layout.row_list_to_do);
            ListView listViewToDo = (ListView) findViewById(R.id.listViewToDo);
            listViewToDo.setAdapter(mAdapter);

            // Load hello items from Azure.
            refreshItemsFromTable();
        }

6. tooensure redirection fonctionne comme prévu, ajoutez hello suivant extrait de _RedirectUrlActivity_ too_AndroidManifest.xml_ :

        <activity android:name="com.microsoft.windowsazure.mobileservices.authentication.RedirectUrlActivity">
            <intent-filter>
                <action android:name="android.intent.action.VIEW" />
                <category android:name="android.intent.category.DEFAULT" />
                <category android:name="android.intent.category.BROWSABLE" />
                <data android:scheme="{url_scheme_of_your_app}"
                    android:host="easyauth.callback"/>
            </intent-filter>
        </activity>

7. Ajoutez too_build.gradle_ redirectUriScheme de votre application Android.

        android {
            buildTypes {
                release {
                    // … …
                    manifestPlaceholders = ['redirectUriScheme': '{url_scheme_of_your_app}://easyauth.callback']
                }
                debug {
                    // … …
                    manifestPlaceholders = ['redirectUriScheme': '{url_scheme_of_your_app}://easyauth.callback']
                }
            }
        }

8. Ajouter des dépendances de toohello com.android.support:customtabs:23.0.1 dans votre build.gradle :

      dependencies {        // ...        compile ’com.android.support:customtabs:23.0.1’    }

9. À partir de hello **exécuter** menu, cliquez sur **exécuter application** toostart hello application et connectez-vous avec votre fournisseur d’identité choisi.

> [!WARNING]
> Hello mentionné le modèle d’URL respecte la casse.  Vérifiez que toutes les occurrences de `{url_scheme_of_you_app}` utilisation hello même casse.

Lorsque vous êtes correctement connecté, application hello doit s’exécuter sans erreurs et vous devez être en mesure de tooquery hello principal service et effectuer des mises à jour toodata.
