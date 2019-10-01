# SubPlugin XML Manifest
This page describes how the XML Manifest of a subplugin is structured.

!> Documentation is incomplete.

### Explainable Example
```xml
<?xml version="1.0" encoding="ISO-8859-1" ?>
<?xml-stylesheet type="text/xsl" href=""?>
<plugin>
    <name>$SUBPLUGIN_NAME</name>
    <displayName>Example Revive Plugin</displayName>
    <creationDate>2019-09-10</creationDate>
    <author>Someone (someone@somewhere.com)</author>
    <authorEmail>someone@somewhere.com</authorEmail>
    <authorUrl>https://someone.com/</authorUrl>
    <license>GNU General Public License v2.0</license>
    <description>This is an example plugin for the Revive Adserver</description>
    <version>0.0.1-dev</version>
    <oxversion>3.2.0-beta-rc3</oxversion>

    <install>
        <syscheck>
        </syscheck>
        <files>
            <file path="{PLUGINPATH}">SUBPLUGIN_NAME.readme.txt</file>
            <file path="{PLUGINPATH}">SUBPLUGIN_NAME.uninstall.txt</file>

            <!-- Plugin www -->
            <file path="{MODULEPATH}$SUBPLUGIN_NAME/">somefile.php</file>
            <file path="{ADMINPATH}/">someotherfile.php</file>
        </files>
        <contents>
            <group name="$SUBPLUGIN_NAME">$PRIORITY</group>
        </contents>
      <configuration>
            <!-- only administrator has permissions to change settings in config file -->
            <setting key="..." type="..." label="..." required="..." size="..." visible="...">$PRIORITY</setting>
        </configuration>
        <schema>
            <mdb2schema>...</mdb2schema>
            <dboschema>db_schema</dboschema>
            <dbolinks>db_schema.links</dbolinks>
            <dataobject>(...).php</dataobject>
        </schema>
        <navigation>
            <checkers>
                <checker class="..." include="(...).php" />
            </checkers>
            <manager>
                <menu addto="..." index="...." link="..." checker="..." helplink="...">$LABEL</menu>
                <menu replace="..." checker="..."></menu>
                ...
            </manager>
            <admin>
                <menu addto="..." index="..." link="..." checker="..." helplink="...">$LABEL</menu>
                <menu replace="..." checker="..."></menu>
                ...
            </admin>
            <advertiser>
                <menu addto="..." index="..." link="..." checker="..." helplink="...">$LABEL</menu>
                <menu replace="..." checker="..."></menu>
                ...
            </advertiser>
            <trafficker>
                <menu addto="..." index="..." link="..." checker="..." helplink="...">$LABEL</menu>
                <menu replace="..." checker="..."></menu>
                ...
            </trafficker>
        </navigation>
    </install>
</plugin>
```
### Explanation:
- `$SUBPLUGIN_NAME`is the subplugin's name and must match and follow the [Subplugin's Structure]()
- `<displayName>`allows to set the Plugin's name (displayed on the admin UI).
- `<creationDate>`allows to set the Plugin's creation date(displayed on the admin UI).
- `<author>`allows to set the Plugin author's name(displayed on the admin UI).
- `<authorEmail>`allows to set the Plugin author's email(displayed on the admin UI).
- `<authorUrl>`sets the Plugin author's url (also displayed on the admin UI).
- `<license>`is used to license the plugin. (displayed in the admin UI).
- `<version>`sets the version of the plugin.
- `<oxversion>`sets the adserver's version which this plugin was designed for.
- `<extends>`if the subplugin extends an existing functionality of the adserver, can be: `api`, `bannerTypeHtml` and so on.
- `<install>`
    - `<syscheck>` ...
    - `<files>` contains all the files packaged in for this subplugin only, if any. This does not include the files of other subplugins or plugins. Each file must be declared here, one by one.
        - `<file>` declares a file packaged in the subplugin, where:
            - `{MODULEPATH}`is equivalent to the plugin's `/plugins/` directory. That's why in this example we use `$SUBPLUGIN_NAME` at the end, to declare files under this subplugin only. 
            - `{ADMINPATH}`is equivalent to the `/www/admin/plugins/$SUBPLUGIN_NAME` directory. 
    - `<schema>`declares the schema modifications this subplugin has.
        - `<mdb2schema>`***tables_`$SUBPLUGIN_NAME`.xml***`</mdb2schema>` specifies the [Database's XML Manifest](). 
        - `<dboschema>`***db_schema***`</dboschema>` declares database schema. (from file path ***plugins/etc/`$SUBPLUGIN_NAME`/etc/DataObjects/db_schema.ini***). See [Database Schema]() for more info.
        - `<dbolinks>`***db_schema.links***`</dbolinks>` declares the schema's foreign keys (from file path ***/plugins/etc/`$SUBPLUGIN_NAME`/etc/DataObjects/db_schema.links.ini***). See [Database Links]() for more info.
        - `<dataobject>` Declares a data object file (`$DATAOBJECT_NAME`). (from file path ***/plugins/etc/`$SUBPLUGIN_NAME`/etc/DataObjects/`$DATAOBJECT_NAME`.php***). See [Database DataObjects]() for more info.
    - `<configuration>`declares the settings of this subplugin, displayed in the admin UI. 
    Only administrator has permissions to change settings in config file. Settings are written to a group section [`$SUBPLUGIN_NAME`]
        - `<setting>`
            * ***key***: is the keyname for this setting. Example:`mySetting1`
            * ***type***: is the "input" type. Example:`checkbox`
            * ***label***: is to describe what this setting does. Example:`Enable ads for vpn users`
            * ***required***: defines if is a required setting`0`for false and `1`for true 
            * ***size***: ...
            * ***visible***: defines the visilibity of the setting`0`for false and `1`for true.
            * `$PRIORITY`is used to define how settings should be ordered (starting from `1`to`999+`
- `<readme>`is used to set the Subplugin's readme text, however if not specified, the readme file from the top-level plugin's directory will be used.
- `<components>`...
- `<navigation>`... [reference](https://github.com/revive-adserver/revive-adserver/blob/master/plugins_repo/openXVideoAds/plugins/etc/videoReport/videoReport.xml)



