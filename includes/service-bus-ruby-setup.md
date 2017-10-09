## <a name="create-a-ruby-application"></a>Création d'une application Ruby
Pour obtenir des instructions, consultez le guide [Création d’une application Ruby sur Azure](../articles/virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).

## <a name="configure-your-application-toouse-service-bus"></a>Configurer votre tooUse application Service Bus
toouse Service Bus, télécharger et utiliser package hello Azure Ruby, qui inclut un ensemble de bibliothèques de commodité qui communiquent avec les services REST de stockage hello.

### <a name="use-rubygems-tooobtain-hello-package"></a>Utiliser le package hello tooobtain RubyGems
1. Ouvrez une interface de ligne de commande, telle que **PowerShell** (Windows), **Terminal** (Mac) ou **Bash** (Unix).
2. Tapez « marque installer azure » dans les dépendances et le marque hello tooinstall hello commande fenêtre.

### <a name="import-hello-package"></a>Importer un package hello
À l’aide de votre éditeur de texte favori, ajoutez hello suivant en haut de toohello de hello Ruby fichier dans lequel vous avez l’intention de toouse stockage :

```ruby
require "azure"
```

## <a name="set-up-a-service-bus-connection"></a>Configuration d’une connexion Service Bus
Les valeurs hello tooset d’espace de noms, nom de hello de code de suivant de hello utilisation clé, clé, signataire et hôte :

```ruby
Azure.configure do |config|
  config.sb_namespace = '<your azure service bus namespace>'
  config.sb_sas_key_name = '<your azure service bus access keyname>'
  config.sb_sas_key = '<your azure service bus access key>'
end
signer = Azure::ServiceBus::Auth::SharedAccessSigner.new
sb_host = "https://#{Azure.sb_namespace}.servicebus.windows.net"
```

La valeur hello espace de noms valeur toohello que vous avez créée au lieu de l’URL complète de hello. Par exemple, utilisez **« votreespacedenomsexemple »** et non « votreespacedenomsexemple.servicebus.windows.net ».
