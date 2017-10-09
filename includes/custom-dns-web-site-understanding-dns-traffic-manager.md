Hello système DNS (Domain Name) est utilisé toolocate les choses sur hello internet. Par exemple, lorsque vous entrez une adresse dans votre navigateur, ou cliquez sur un lien sur une page web, il utilise domaine de hello tootranslate DNS en adresse IP. adresse IP de Hello est comme une adresse postale, mais il n’est pas très humaine convivial. Par exemple, il est beaucoup plus facile tooremember un nom DNS, tel que **contoso.com** que celui qu’elle est tooremember une adresse IP comme 192.168.1.88 ou 2001:0:4137:1f67:24a2:3888:9cce:fea3.

Hello système DNS est basé sur *enregistrements*. Les enregistrements associent un *nom*spécifique, tel que **contoso.com**, à une adresse IP ou un autre nom DNS. Lorsqu’une application, comme un navigateur web, recherche un nom dans DNS, il trouve hello enregistrement et utilise ce que qu’elle pointe tooas hello adresse. Si hello valeur points toois une adresse IP, navigateur de hello utilise cette valeur. S’il pointe le nom DNS de tooanother, puis application hello a toodo résolution à nouveau. En fin de compte, toute résolution de nom génère une adresse IP.

Lorsque vous créez un site Web Azure, un nom DNS est automatiquement attribué toohello site. Ce nom prend la forme hello  **&lt;yoursitename&gt;. azurewebsites.net**. Lorsque vous ajoutez à votre site Web comme point de terminaison Azure Traffic Manager, votre site Web est ensuite accessible via hello  **&lt;yourtrafficmanagerprofile&gt;. trafficmanager.net** domaine.

> [!NOTE]
> Lorsque votre site Web est configuré comme un point de terminaison Traffic Manager, vous allez utiliser hello **. trafficmanager.net** adresse lors de la création des enregistrements DNS.
> 
> Seuls les enregistrements CNAME peuvent être utilisés avec Traffic Manager.
> 
> 

Il existe également plusieurs types d’enregistrements, chacun avec leurs propres fonctions et les limitations, mais pour les sites Web configurés tooas points de terminaison Traffic Manager, nous avons uniquement en charge sur un ; *CNAME* enregistrements.

### <a name="cname-or-alias-record"></a>Enregistrement CNAME ou d'alias
Un enregistrement CNAME associe un *spécifique* nom DNS, tel que **mail.contoso.com** ou **www.contoso.com**, nom de domaine (canonique) tooanother. Dans les cas de hello des sites Web d’Azure à l’aide de Traffic Manager, le nom de domaine canonique hello est hello  **&lt;myapp >. trafficmanager.net** nom de domaine de votre profil Traffic Manager. Une fois créé, hello CNAME crée un alias pour hello  **&lt;myapp >. trafficmanager.net** nom de domaine. Hello entrée CNAME peut résoudre l’adresse IP de toohello de votre  **&lt;myapp >. trafficmanager.net** nom de domaine automatiquement, donc si l’adresse IP de hello du site Web de hello change, vous n’avez pas n’importe quelle action aux tootake.

Une fois que le trafic arrive à Traffic Manager, il achemine ensuite hello trafic tooyour du site Web, à l’aide de la méthode, pour qu'il est configuré d’équilibrage de charge de hello. Il s’agit de site Web de tooyour toovisitors totalement transparente. Ils voient uniquement le nom de domaine personnalisé hello dans leur navigateur.

> [!NOTE]
> Des bureaux d’enregistrement de domaine vous permettre uniquement de sous-domaines de toomap lors de l’utilisation d’un enregistrement CNAME, tel que **www.contoso.com**et non racine, les noms tels que **contoso.com**. Pour plus d’informations sur les enregistrements CNAME, consultez la documentation hello fournie par votre bureau d’enregistrement, <a href="http://en.wikipedia.org/wiki/CNAME_record">hello Wikipédia sur l’enregistrement CNAME</a>, ou hello <a href="http://tools.ietf.org/html/rfc1035">IETF de noms de domaine - implémentation et spécification</a> document.
> 
> 

