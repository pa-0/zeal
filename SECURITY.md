Docset Generation Guide
=======================

_Instructions on how to generate docsets (for [Dash](dash)) are found below. There is no method that is best for every case, so you'll have to consider all and decide which is the best for you. When your docset is ready, please [contribute it](https://github.com/Kapeli/Dash-User-Contributions#contribute-a-new-docset) to Dash._

Generate docsets from:
----------------------

*   [1. Swift DocC Documentation](#swift)
*   [2. Python, Sphinx or PyDoctor-Generated Documentation](#python)
*   [3. Javadoc-Generated Documentation](#javadoc)
*   [4. RDoc or Yard-Generated Documentation](#rdoc)
*   [5. Scaladoc-Generated Documentation](#scaladoc)
*   [6. GoDoc-Generated Documentation](#godoc)
*   [7. HexDoc-Generated Documentation](#exdoc)
*   [8. DartDoc-Generated Documentation](#dartdoc)
*   [9. Haddock-Generated Documentation](#haddock)
*   [10. Rust Package Documentation (Cargo)](#rustcargo)
*   [11. JSDoc Comments](#jsdoc)
*   [12. Doxygen (Source Files: C, C++, C#, PHP, Objective-C, Java, Python)](#doxygen)
*   [13. Any HTML Documentation](#dashDocset)

*   [13.1. Create the Docset Folder](#setUpFolderStructure)
*   [13.2. Copy the HTML Documentation](#copyDocumentation)
*   [13.3. Create the Info.plist File](#infoplist)
*   [13.4. Create the SQLite Index](#createsqlite)
*   [13.5. Populate the SQLite Index](#fillsqlite)

*   [13.5.1. Supported Entry Types](#supportedentrytypes)

*   [13.6. Table of Contents Support (optional)](#tableofcontents)

Generation script examples:
---------------------------

*   [1. Python](#pythonExample)
*   [2. Ruby](#rubyExample)
*   [3. Objective-C](#objcExample)
*   [4. Node.js](#nodeExample)
*   [5. PHP](#phpExample)

Improve your docset:
--------------------

*   [1. Contribute it to Dash](#contributetodash)
*   [2. Set a Main Page](#settingindexpage)
*   [3. Add an Icon](#addingicon)
*   [4. Support Online Redirection](#onlineRedirection)
*   [5. Support Docset Playgrounds](#docsetPlaygrounds)
*   [6. Enable JavaScript](#enableJavascript)
*   [7. Enable or Disable Full-Text Search](#fts)
*   [8. Host a Docset Feed](#dashdocsetfeed)
*   [9. Share a Docset Feed](#sharedocsetfeed)

Docset Sources[#](#docsetSources)
---------------------------------

### 1. Swift DocC Documentation[#](#swift)

Dash can open DocC archives, as well as generate DocC for any Swift Package in Preferences > Downloads > Swift Docsets.

### 2. Python, Sphinx or PyDoctor-Generated Documentation[#](#python)

You can install docsets for any Sphinx-generated docs from Preferences > Downloads > Python Docsets.

Alternatively, use [http://pypi.python.org/pypi/doc2dash](http://pypi.python.org/pypi/doc2dash) to generate docsets from Sphinx or PyDoctor-generated documentation. When you're done generating your docset, check out some tips on [how to improve it](#improveDocset).

### 3. Javadoc-Generated Documentation[#](#javadoc)

You can install docsets for Java libraries that are on [Maven.org](http://maven.org) from Preferences > Downloads > Java Docsets.

Use [https://github.com/Kapeli/javadocset](https://github.com/Kapeli/javadocset#readme) to generate docsets from Javadoc-generated documentation. When you're done generating your docset, check out some tips on [how to improve it](#improveDocset).

### 4. RDoc or Yard-Generated Documentation[#](#rdoc)

You can install docsets for any Ruby Gem from Preferences > Downloads > Ruby Docsets.

### 5. Scaladoc-Generated Documentation[#](#scaladoc)

You can install docsets for Scala libraries that are on [Maven.org](http://maven.org) from Preferences > Downloads > Scala Docsets.

Use [sbt-dash](https://github.com/jastice/sbt-dash) or [mkscaladocset](https://bitbucket.org/inkytonik/mkscaladocset) to generate docsets from Scaladoc-generated API documentation. Use [scala-dash](https://github.com/cvogt/scala-dash) to generate docsets for Scala manuals. When you're done generating your docset, check out some tips on [how to improve it](#improveDocset).

### 6. GoDoc-Generated Documentation[#](#godoc)

You can install docsets for any Go Package from Preferences > Downloads > Go Docsets.

Use [https://github.com/wuudjac/godocdash](https://github.com/wuudjac/godocdash#readme) to generate docsets from GoDoc-generated documentation. When you're done generating your docset, check out some tips on [how to improve it](#improveDocset).

### 7. HexDoc-Generated Documentation[#](#exdoc)

You can install docsets for any Hex Package from Preferences > Downloads > Hex Docsets.

### 8. DartDoc-Generated Documentation[#](#dartdoc)

You can install docsets for any Dart Package from Preferences > Downloads > Dart Docsets.

### 9. Haddock-Generated Documentation[#](#haddock)

You can install docsets for any Haskell Package from Preferences > Downloads > Haskell Docsets.

### 10. Rust Package Documentation (Cargo)[#](#rustcargo)

You can install docsets for any Rust crate from Preferences > Downloads > Rust Docsets.

Use [cargo-docset](https://github.com/Robzz/cargo-docset) or [rsdocs-dashing](https://github.com/hobofan/rsdocs-dashing) to generate docsets for Rust packages. When you're done generating your docset, check out some tips on [how to improve it](#improveDocset).

### 11. JSDoc Comments[#](#jsdoc)

Use [https://github.com/theasta/jsdoc-dash-template](https://github.com/theasta/jsdoc-dash-template#readme) to generate docsets from JSDoc comments. When you're done generating your docset, check out some tips on [how to improve it](#improveDocset).

### 12. Doxygen (Source Files: C, C++, C#, PHP, Obj-C, Java, Python)[#](#doxygen)

[Doxygen](http://www.stack.nl/~dimitri/doxygen/) can generate docsets from source files of C, C++, C#, PHP, Objective-C, Java, Python (and some others).

These are the entries you need to add into your Doxygen config file to make it generate a docset (note: the last 3 entries are optional):

```
GENERATE_DOCSET   = YES
DISABLE_INDEX     = YES 
SEARCHENGINE      = NO
GENERATE_TREEVIEW = NO
```

When Doxygen is done generating the documentation, run `make` inside the generated folder. Note: Doxygen requires `docsetutil`, which is no longer available starting with Xcode 9.3. You need to either install Xcode 9.2 or older, or check out this [GitHub repo](https://github.com/SwiftDocOrg/DocSetUtil) for an alternative.

Don't forget to check out some tips on [how to improve your docset](#improveDocset).

### 13. Any HTML Documentation[#](#dashDocset)

Docsets are essentially just a folder containing the HTML documentation and a SQLite database that indexes the files.

If the HTML docs you want to index are well-formatted, it might be easier to generate the docset using [Dashing](https://github.com/technosophos/dashing#readme) or [dash-docset-builder](https://github.com/godbout/dash-docset-builder) instead of writing your own generation script.

You can also use the general-purpose Docset Generator included in Dash, from Dash's Preferences > Downloads > Docset Generator.

#### 13.1. Create the Docset Folder[#](#setUpFolderStructure)

The docset folder structure can be created using this Terminal command:

mkdir -p <docset name>.docset/Contents/Resources/Documents/

You can also manually create the docset structure if you want, they're just folders.

#### 13.2. Copy the HTML Documentation[#](#copyDocumentation)

Copy the HTML documentation you already have to this folder:

<docset name>.docset/Contents/Resources/Documents/

#### 13.3. Create the Info.plist File[#](#infoplist)

Download and edit this sample [Info.plist](resources/Info.plist) and place it in the `<docset name>.docset/Contents/` folder. Editing should be straightforward, just set the values to whatever name you want for your docset.

#### 13.4. Create the SQLite Index[#](#createsqlite)

Create a SQLite database in the file `<docset name>.docset/Contents/Resources/docSet.dsidx` with the following query:

CREATE TABLE searchIndex(id INTEGER PRIMARY KEY, name TEXT, type TEXT, path TEXT);

Recommended: you can easily prevent adding duplicate entries to the index by also using this query:

CREATE UNIQUE INDEX anchor ON searchIndex (name, type, path);

#### 13.5. Populate the SQLite Index[#](#fillsqlite)

You need to create a script (or application or whatever) that will go through your HTML documentation and add appropriate rows into the SQLite database. Rows can be added using this query:

INSERT OR IGNORE INTO searchIndex(name, type, path) VALUES ('name', 'type', 'path');

The values are:

*   `name` is the name of the entry. For example, if you are adding a class, it would be the name of the class. This is the column that Dash searches.
*   `type` is the type of the entry. For example, if you are adding a class, it would be "Class". For a list of types that Dash recognises, see below.
*   `path` is the relative path towards the documentation file you want Dash to display for this entry. It can contain an anchor (#). Alternatively, Dash also supports `http://` URL entries.

You can find a few generation script examples [here](#scriptExamples).

##### 13.5.1. Supported Entry Types[#](#supportedentrytypes)

*   Annotation
*   Attribute
*   Binding
*   Builtin
*   Callback
*   Category
*   Class
*   Command
*   Component
*   Constant
*   Constructor
*   Define
*   Delegate
*   Diagram
*   Directive
*   Element
*   Entry
*   Enum
*   Environment
*   Error
*   Event
*   Exception
*   Extension
*   Field
*   File
*   Filter
*   Framework
*   Function
*   Global
*   Guide
*   Hook
*   Instance
*   Instruction
*   Interface
*   Keyword
*   Library
*   Literal
*   Macro
*   Method
*   Mixin
*   Modifier
*   Module
*   Namespace
*   Notation
*   Object
*   Operator
*   Option
*   Package
*   Parameter
*   Plugin
*   Procedure
*   Property
*   Protocol
*   Provider
*   Provisioner
*   Query
*   Record
*   Resource
*   Sample
*   Section
*   Service
*   Setting
*   Shortcut
*   Statement
*   Struct
*   Style
*   Subroutine
*   Tag
*   Test
*   Trait
*   Type
*   Union
*   Value
*   Variable
*   Word

Please contact Dash if none of the currently supported types are suitable for what you're trying to index.

#### 13.6. Table of Contents Support (optional)[#](#tableofcontents)

To allow easy navigation inside a large page, Dash is able to show a table of contents at the bottom left. This feature is described in the [user guide](dash_guide#tableOfContents).

Please note that adding table of contents support is a bit tricky (and optional).

When Dash displays a documentation page, it also looks for special anchors inside the HTML and generates a table of contents. To add table of contents support, you need to go through all the HTML pages and insert anchors in a format that Dash understands. The anchors need to be inserted in the HTML pages themselves.

The format for the anchors is:

```html
<a name="//apple_ref/cpp/Entry Type/Entry Name" class="dashAnchor"></a>
```

The only things that you need to change in the format above are:

*   `Entry type` - one of the [supported entry types](#supportedentrytypes).
*   `Entry name` - the name that is shown by Dash in the table of contents. Preferably, it should be [percent escaped](http://en.wikipedia.org/wiki/Percent-encoding).

You can see an example of how to insert anchors at [https://github.com/jkozera/zeal/blob/master/gendocsets/extjs/parse.py](https://github.com/zealdocs/zeal/blob/aaa5dff85772921fc91397aa449e0f5316334506/gendocsets/extjs/parse.py#L182) (in Python).

You'll also need to add this entry in the docset's Info.plist:

```xml
<key>DashDocSetFamily</key>
<string>dashtoc</string>
```

Some notes:

*   You should URL encode (percent escape) the "Entry Name" if it contains symbols.
*   After changing the Info.plist, you should remove the docset from Preferences > Docsets and re-add it.
*   Do not hesitate to contact me if you are having problems with this. The process is a bit confusing.

Generation Script Examples[#](#scriptExamples)
----------------------------------------------

### 1. Python[#](#pythonExample)

See [https://github.com/drbraden/pgdash](https://github.com/drbraden/pgdash).

### 2. Ruby[#](#rubyExample)

See [https://github.com/Kapeli/erlang-docset](https://github.com/Kapeli/erlang-docset/blob/master/src/generate.rb).

### 3. Objective-C[#](#objcExample)

See [https://github.com/Kapeli/javadocset](https://github.com/Kapeli/javadocset).

### 4. Node.js[#](#nodeExample)

See [https://github.com/exlee/d3-dash-gen](https://github.com/exlee/d3-dash-gen).

### 5. PHP[#](#phpExample)

See [https://github.com/akirk/dash-phpunit](https://github.com/akirk/dash-phpunit).

Improve Your Docset[#](#improveDocset)
--------------------------------------

### 1. Contribute it to Dash[#](#contributetodash)

See [https://github.com/Kapeli/Dash-User-Contributions](https://github.com/Kapeli/Dash-User-Contributions#contribute-a-new-docset).

### 2. Set a Main Page[#](#settingindexpage)

You can specify the main page that Dash shows when the user opens a docset by adding the following to Info.plist:

```xml
<key>dashIndexFilePath</key>
<string>index.html</string>
```
The path should be relative to the `Documents` folder inside the docset. It can also be a `http://` URL.

After adding the main page, remove and re-add the docset in Dash's Preferences.

### 3. Add an Icon[#](#addingicon)

To set a custom icon for your docset, simply add a `icon.png` file directly inside the docset bundle. For example, the file path would be `<docset name>.docset/icon.png`.

The size of the icon should be 16x16 or 32x32. For Retina display support, you can either use a single 32x32 icon or 2 separate icons: `icon.png` (16x16) and `icon@2x.png` (32x32).

After adding the icon, remove and re-add the docset in Dash's Preferences.

### 4. Support Online Redirection[#](#onlineRedirection)

Starting with version 3.0, Dash users can open the online version of pages inside docsets. To do that, Dash needs to know where to find the online pages for your docset.

You have 2 options to support online redirection:

*   Set the `DashDocSetFallbackURL` key in your docset's Info.plist. The value should be the base URL of the docs. Example: `https://docs.python.org/3/library/`
*   Alternatively, add a HTML comment inside each and every HTML file of your docset. The comment needs to be added next to the `<html>` tag of the pages and should look like this:

```html    
<html><!-- Online page at https://docs.python.org/3/library/intro.html -->
```


### 5. Support Docset Playgrounds[#](#docsetPlaygrounds)

Starting with version 4.0, Dash now shows a play button next to docsets which takes users to a playground for the language/framework of the docset. To support it you need to:

*   Set the `DashDocSetPlayURL` key in your docset's Info.plist. The value should be the URL of the docset playground. Example: `[https://repl.it/F9J7/1](https://repl.it/F9J7/1)` for the Swift docset.

### 6. Enable JavaScript[#](#enableJavascript)

By default, Dash does not allow external `.js` scripts. You can enable them by adding this entry to the docset's Info.plist:

<key>isJavaScriptEnabled</key><true/>

After adding this entry, remove and re-add the docset in Dash's Preferences.

### 7. Enable or Disable Full-Text Search[#](#fts)

Full-text search is disabled for docsets by default and users can enable it from within Dash's interface. If you want, you can have your docset default to having full-text search enabled by adding the following key to `Info.plist`:

<key>DashDocSetDefaultFTSEnabled</key><true/>

You can also disable full-text search support completely for your docset (i.e. users won't be able to enable it at all) by adding this key to `Info.plist`:

<key>DashDocSetFTSNotSupported</key><true/>

### 8. Host a Docset Feed[#](#dashdocsetfeed)

**Important:** It is highly recommended that you [contribute your docset](https://github.com/Kapeli/Dash-User-Contributions#contribute-a-new-docset) to Dash instead of setting up a docset feed. Docset feeds should only be used for docsets which only you, your team or very few users find useful.

Documentation feeds allow Dash users to conveniently install and update docsets. If you want to distribute a docset you should set up a feed for it, so that you'll be able to update it in the future.

Dash documentation feeds are very simple, check one out: [NodeJS\_Sample.xml](resources/NodeJS_Sample.xml).

It's a XML file that contains the following:

*   A root `<entry>` element
    *   A `<version>` element. You can use any versioning system you want. Dash will use string comparison to determine whether or not to download an update.
    *   One or several `<url>` elements. These point to the URL of the archived docset.

To archive your docset, use the following command:

tar --exclude='.DS\_Store' -cvzf <docset name>.tgz <docset name>.docset

Currently only one docset per feed is supported (only one `<entry>`).

### 9. Share a Docset Feed[#](#sharedocsetfeed)

You can share docset feeds using a custom URL scheme, which will allow Dash to subscribe to that feed with a single click.

dash-feed://<URL encoded feed URL>

By URL encoded, I mean percent-encoding (e.g. what you’d get by clicking the encode button [here](http://meyerweb.com/eric/tools/dencoder/)).

Example:

*   [dash-feed://http%3A%2F%2Fkapeli.com%2Ffeeds%2FNodeJS.xml](dash-feed://http%3A%2F%2Fkapeli.com%2Ffeeds%2FNodeJS.xml)

*   Subscribes to the [http://kapeli.com/feeds/NodeJS.xml](//kapeli.com/feeds/NodeJS.xml) feed

[License Agreement](//kapeli.com/license_agreement)[Privacy Policy](//kapeli.com/privacy_policy)
