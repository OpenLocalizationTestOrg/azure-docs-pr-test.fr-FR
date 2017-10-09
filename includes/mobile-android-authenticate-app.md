
1. <span data-ttu-id="d2b2f-101">Ouvrez le projet de hello dans Android Studio.</span><span class="sxs-lookup"><span data-stu-id="d2b2f-101">Open hello project in Android Studio.</span></span>

2. <span data-ttu-id="d2b2f-102">Dans **Explorateur de projets** dans Android Studio, ouvrez le fichier ToDoActivity.java de hello et ajouter hello suivant les instructions d’importation :</span><span class="sxs-lookup"><span data-stu-id="d2b2f-102">In **Project Explorer** in Android Studio, open hello ToDoActivity.java file and add hello following import statements:</span></span>

        import java.util.concurrent.ExecutionException;
        import java.util.concurrent.atomic.AtomicBoolean;

        import android.content.Context;
        import android.content.SharedPreferences;
        import android.content.SharedPreferences.Editor;

        import com.microsoft.windowsazure.mobileservices.authentication.MobileServiceAuthenticationProvider;
        import com.microsoft.windowsazure.mobileservices.authentication.MobileServiceUser;

3. <span data-ttu-id="d2b2f-103">Ajouter hello suivant de méthode toohello **ToDoActivity** classe :</span><span class="sxs-lookup"><span data-stu-id="d2b2f-103">Add hello following method toohello **ToDoActivity** class:</span></span>

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

    <span data-ttu-id="d2b2f-104">Ce code crée un Bonjour de toohandle méthode processus d’authentification Google.</span><span class="sxs-lookup"><span data-stu-id="d2b2f-104">This code creates a method toohandle hello Google authentication process.</span></span> <span data-ttu-id="d2b2f-105">Une boîte de dialogue affiche hello des ID d’utilisateur de hello authentifié.</span><span class="sxs-lookup"><span data-stu-id="d2b2f-105">A dialog displays hello ID of hello authenticated user.</span></span> <span data-ttu-id="d2b2f-106">Vous pouvez agir uniquement si l’authentification a réussi.</span><span class="sxs-lookup"><span data-stu-id="d2b2f-106">You can only proceed on a successful authentication.</span></span>

    > [!NOTE]
    > <span data-ttu-id="d2b2f-107">Si vous utilisez un fournisseur d’identité autre que Google, modifiez la valeur hello passé toohello **connexion** tooone méthode Hello valeurs suivantes : _MicrosoftAccount_, _Facebook_, _Twitter_, ou _windowsazureactivedirectory_.</span><span class="sxs-lookup"><span data-stu-id="d2b2f-107">If you are using an identity provider other than Google, change hello value passed toohello **login** method tooone of hello following values: _MicrosoftAccount_, _Facebook_, _Twitter_, or _windowsazureactivedirectory_.</span></span>

4. <span data-ttu-id="d2b2f-108">Bonjour **onCreate** (méthode), ajouter hello après la ligne de code après le code hello qui instancie hello `MobileServiceClient` objet.</span><span class="sxs-lookup"><span data-stu-id="d2b2f-108">In hello **onCreate** method, add hello following line of code after hello code that instantiates hello `MobileServiceClient` object.</span></span>

        authenticate();

    <span data-ttu-id="d2b2f-109">Cet appel démarre le processus d’authentification hello.</span><span class="sxs-lookup"><span data-stu-id="d2b2f-109">This call starts hello authentication process.</span></span>

5. <span data-ttu-id="d2b2f-110">Déplacer hello restant code après `authenticate();` Bonjour **onCreate** tooa méthode nouvelle **createTable** méthode :</span><span class="sxs-lookup"><span data-stu-id="d2b2f-110">Move hello remaining code after `authenticate();` in hello **onCreate** method tooa new **createTable** method:</span></span>

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

6. <span data-ttu-id="d2b2f-111">tooensure redirection fonctionne comme prévu, ajoutez hello suivant extrait de _RedirectUrlActivity_ too_AndroidManifest.xml_ :</span><span class="sxs-lookup"><span data-stu-id="d2b2f-111">tooensure redirection works as expected, add hello following snippet of _RedirectUrlActivity_ too_AndroidManifest.xml_:</span></span>

        <activity android:name="com.microsoft.windowsazure.mobileservices.authentication.RedirectUrlActivity">
            <intent-filter>
                <action android:name="android.intent.action.VIEW" />
                <category android:name="android.intent.category.DEFAULT" />
                <category android:name="android.intent.category.BROWSABLE" />
                <data android:scheme="{url_scheme_of_your_app}"
                    android:host="easyauth.callback"/>
            </intent-filter>
        </activity>

7. <span data-ttu-id="d2b2f-112">Ajoutez too_build.gradle_ redirectUriScheme de votre application Android.</span><span class="sxs-lookup"><span data-stu-id="d2b2f-112">Add redirectUriScheme too_build.gradle_ of your Android application.</span></span>

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

8. <span data-ttu-id="d2b2f-113">Ajouter des dépendances de toohello com.android.support:customtabs:23.0.1 dans votre build.gradle :</span><span class="sxs-lookup"><span data-stu-id="d2b2f-113">Add com.android.support:customtabs:23.0.1 toohello dependencies in your build.gradle:</span></span>

      <span data-ttu-id="d2b2f-114">dependencies {        // ...        compile ’com.android.support:customtabs:23.0.1’    }</span><span class="sxs-lookup"><span data-stu-id="d2b2f-114">dependencies {        // ...        compile 'com.android.support:customtabs:23.0.1'    }</span></span>

9. <span data-ttu-id="d2b2f-115">À partir de hello **exécuter** menu, cliquez sur **exécuter application** toostart hello application et connectez-vous avec votre fournisseur d’identité choisi.</span><span class="sxs-lookup"><span data-stu-id="d2b2f-115">From hello **Run** menu, click **Run app** toostart hello app and sign in with your chosen identity provider.</span></span>

> [!WARNING]
> <span data-ttu-id="d2b2f-116">Hello mentionné le modèle d’URL respecte la casse.</span><span class="sxs-lookup"><span data-stu-id="d2b2f-116">hello URL Scheme mentioned is case-sensitive.</span></span>  <span data-ttu-id="d2b2f-117">Vérifiez que toutes les occurrences de `{url_scheme_of_you_app}` utilisation hello même casse.</span><span class="sxs-lookup"><span data-stu-id="d2b2f-117">Ensure that all occurrences of `{url_scheme_of_you_app}` use hello same case.</span></span>

<span data-ttu-id="d2b2f-118">Lorsque vous êtes correctement connecté, application hello doit s’exécuter sans erreurs et vous devez être en mesure de tooquery hello principal service et effectuer des mises à jour toodata.</span><span class="sxs-lookup"><span data-stu-id="d2b2f-118">When you are successfully signed in, hello app should run without errors, and you should be able tooquery hello back-end service and make updates toodata.</span></span>
