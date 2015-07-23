# Remplacement instantané de la langue coté client
### Change la langue sans recharger la page ou faire une requête serveur. Voir l'exemple fournit dans index.html

Ce  plugin JQuery permet de créer plusieurs version linguistique de chaque phrase de votre contenu.  

La traduction se fait a partir d'un langage par défaut comme l'anglais.

### Utilisé par de grandes entreprises
![Logos](http://www.irrelon.com/assets/logos_lang.png)

## Fonctionalités
* Remplacement instantané de la langue - pas de rechargement de page
* Traduction automatique des zones de vos pages (e.g. chargé via AJAX ou ajouté via jQuery)
* Persistance du langage entre les pages et rechargement via cookies (requière jquery-cookie.js)
* Supporte les expression régulières / remplace depuis des traductions qui ne sont pas des tokens
* Supporte le changement d'URL des images
* Event hooks pour personaliser son code
* Pas de temps d'attente ou de timeout, juste un code haute performance
 
## Qui a développé ça ?
Ce plugin et tout le code relatif ont été créé par Irrelon Software Limited, une entreprise britanique avec pour mission de créer des applications web fantastiques et de repousser les frontières du développemetn web. Venez nous voir sur http://www.irrelon.com.

#### LinkedIn
http://uk.linkedin.com/pub/rob-evans/25/b94/8a5/

#### Traduction française du code
https://github.com/emgepub/jquery-lang-js

# Changelog
2015-01-09 - Version 2.8
* Added support for changing images when the language changes

2015-01-07 - Version 2.7
* Removed console.log() calls so that old versions of Internet Explorer won't break

2014-06-06 - Version 2.6
* Changed _getTextNodes & _setTextNodes methods to work under IE8. _getTextNodes returns now array of objects where every object have two properties:
	- node - current text node
	- langDefaultText - remember data of current text node 

2014-04-19 - Version 2.5
* Changed dynamically loaded language packs to JSON format. This allows the packs to be loaded by other programming languages such as PHP that can natively interpret JSON but not JavaScript.

2014-02-22 - Version 2.4
* Added dynamic loading of language packs so they don't need to be loaded up front, saving on HTTP requests and memory usage

2014-02-02 - Version 2.3
* Fixed bug when switching from non-default language to other non-default language

2014-02-01 - Version 2.2
* Check that a language pack actually exists before trying to switch to it
* Allow disabling event firing so dynamic elements wont fire update events
* Allow cookies to override passed current language on constructor if passing true as third arg to new Lang()
* Fix to allow auto-translate when using jQuery appendTo() method
* Fix for dynamic translation of root-element text nodes

2014-02-01 - Version 2.1
* Fixed break in jQuery chaining
* Added cookies for persistence when $.cookie exists
* Supports automatic translation for dynamically added content (when added via jQuery)
* Added support for regular expression matches
* Added support for translating text nodes mixed with html nodes

2014-01-31 - Version 2.0
* Complete plugin re-write

# Comment l'utiliser

*Si vous souhaitez que la sélection de la langue soit persistante entre les pages, vérifiez que vous avez inclus le plugin jquery-cookie plugin disponible depuis: https://github.com/carhartl/jquery-cookie.

Incluez le script (dans votre head).

    <script src="js/jquery-lang.js" charset="utf-8" type="text/javascript"></script>

Et insérez le code suivant dans votre page HTML :

    <script type="text/javascript">
    // initialise le plugin de langue et configure par defaut en anglais (en)
	window.lang = new Lang('en');
    </script>

# Charger les packs de langue dynmiquement (Recommandé)
A la place de charger tous les packs de langue d'un coups, il est préférable de charger un pack que lorsque le client le demande. 

Le plugin vous permet simplement de définir les packs et les chemins d'accès et il se chargera automatiquement de le charger à la demande. Pour définir un langage de pack dynamique, appelez la méthode lang.dynamic() après que le plugin soit chargé et initialisé :

	// Définie le pack de langue thai comme dynamique pack afin qu'il soit chargé à la demande
	// si l'utilisateur demande à changer de langue pour ce langage. On passe les deux lettres (iso)
	// et le chemin d'accès du pack de langue thai
	window.lang.dynamic('th', 'js/langpack/th.json');

## Inclure les packs de langue Language Packs Up-Front (Optional)
*The recommended way to use language packs is to define them dynamically (see Loading Language Packs Dynamically above)*

You can include any language pack you have created up-front so they are ready to use straight away on your page. If you
do it this way you must make the language pack a JS file and include a line of code to insert the pack into the Lang 
prototype. See the ./langPack/nonDynamic.js file for an example. Pay attention to the regex section as well as this needs
to define regex patterns directly instead of as strings.

	<script src="js/langpack/nonDynamic.js" charset="utf-8" type="text/javascript"></script>

# Defining which elements to translate

In the HTML content itself you can denote an element as being available for translation by adding a "lang"
attribute with the language of the content as such:

    <span lang="en">Translate me</span>

Or any element with some content such as:

    <select name="testSelect">
        <option lang="en" value="1">An option phrase to translate</option>
        <option lang="en" value="2">Another phrase to translate</option>
    </select>

# Button elements

The plugin will automatically translate button element text when defined like this:

    <button lang="en">Some button text</button>

# Placeholder text

You can also translate placeholder text like this:

    <input type="text" placeholder="my placeholder text" lang="en" />

When you change languages, the plugin will update the placeholder text where a translation exists.

# Translating other text in JavaScript such as alert() calls

If you need to know the current translation value of some text in your JavaScript code such as when calling
alert() you can use the translate() method:

    alert(window.lang.translate('Some text to translate'));

# Dynamic content

If you load content dynamically and add it to the DOM using jQuery the plugin will AUTOMATICALLY translate
to the current language. Ensure you have added "lang" attributes to any HTML that you want translated BEFORE
you add it to the DOM.

# Switching languages

To switch languages simply call the .change() method, passing the two-letter language code to switch to. For
instance here is a switcher that will change between English and Thai as used in the example page:

    <a href="#lang-en" onclick="window.lang.change('en'); return false;">Switch to English</a> | <a href="#lang-en" onclick="window.lang.change('th'); return false;">Switch to Thai</a>

The onclick event is the only part that matters, you can apply the onclick to any element you prefer.

# Define a language pack

Language packs are defined in JSON files and are added to the plugin like so:

    {
    	// Define token (exact phrase) replacements here
    	"token": {
			"Property Search":"ค้นหา",
			"Location":"สถานที่ตั้ง",
			"Budget":"งบประมาณ",
			"An option phrase to translate":"งบประมาณงบประมาณสถานที่ตั้ง",
		},
		// Define regular expression replacements here
		"regex": [
			["My regex", "i", "someReplacement"]
		]
    }

That example just defined a language pack to translate from the default page language English into Thai (th).
Each property inside the token object has a key that is the English phrase, then the value is the Thai equivalent.

The regex section allows you to specify regular expressions to use for matching and replacement. The regular expressions
are only evaluated IF a token-based replacement is not found for a section of text.

It's that simple!

### Using Dynamic Packs
When you call lang.change('th'), the plugin will check if the language pack is already loaded and if not, will load
the pack first before changing languages. Once the pack file has been loaded the plugin will change to that language.

Loading languages dynamically is only done when the the change() method is called. This means if you request a
translation of a string via the translate() method BEFORE the language pack for that language is loaded the translation
will fail.

If you require a language pack to be loaded and don't want to change the page language you can request loading the pack
manually by calling the loadPack() method like so:

	lang.loadPack('th');

If you need to know when the pack has been loaded pass a callback method:

	lang.loadPack('th', function (err) {
		if (!err) {
			// The language pack loaded
		} else {
			// There was an error loading the pack
		}
	});

# Translating Custom Element Attributes
The plugin maintains a list of attributes that will automatically translate and you can specify your own custom attributes too. The attributes that are translated by default are:

* title
* alt
* placeholder
* href

You can specify custom attributes that will be translated by adding them to the attrList property of the lang-js instance. For example to auto-translate an attribute called 'data-name' you would add this after lang-js has been included on your page:

	Lang.prototype.attrList.push('data-name');

# Bugs, Issues, Questions, Contacts et Feature Requests
Postez vos demandes via le système d'Issus de Github de ce répertoire

# Améliorations et Pull Requests

Nous encourageons activement à améliorer ce plugin et à nous envoyez des pull requests pour partager votre fabuleux travail ! Vérifiez néanmoins que les changements :

1. Ne soientt pas cassant (Breaking-change)
2. Soient testés avec la dernière version
3. Soient documentés avec la JSDoc standard

Thank you to everyone who takes their time to write updates to the plugin!

# Roadmap

* **COMPLETED** - Dynamic language pack loading
* **COMPLETED** - Swap image assets based on language
* Swap video assets based on language

# License

This plugin and all code contained is Copyright 2014 Irrelon Software Limited. You are granted a license to use
this code / software as you wish, free of charge and free of restrictions under the MIT license. See the source
code file jquery-lang.js for the full license details.

Si vous aimez ce projet, svp Flattr-ing le! http://bit.ly/qCEbTC

Ce projet est mise à jour et maintenu par:

Irrelon Software Limited
http://www.irrelon.com
