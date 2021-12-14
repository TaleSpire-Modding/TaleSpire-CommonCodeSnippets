# DEVELOPER CONVENTIONS:

The following is a list of recommended conventions to use when creating plugins or asset bundles.
There are not absolutely necessary but following them will mean maximum compatibility with other
plugins and lower changes of issues.

## Asset Naming

Assets need to have unique names in order to be compatible with plugins like EAR, CMP and Replicator.
Since there are more and more asset packs being shared we need to ensure that our asset names are
unique but use short and readable names for plugins like CMP and Replicator where the asset name
needs to be entered.

The suggested naming convention for assets is:

```creator_initals content_name sequence_number``` such as ```laAssassin01```

The initials will ensure the asset is unique between other creators creating the same type of asset
and the sequence numeber at the end will ensure that the same creator can make more than one version
of the content. Since the sequence number is specific to the content creator each creator can track
their own number.

If you are going to make content, please register your initials with Lord Ashes (tell him using the
TaleSpire Modding Discord) so that others don't use the same initials. Registered initials will be
listed here:

```
la = LordAshes
hf = HolloFox
sc = Scott Cross
ph = Phenex
```


## Size Convention

When creating assets that are not Medium size (1x1 tile), create the asset as if it was a medium sized
creature and the use the TaleSpire base to make it larger or smaller. This ensures that larger or
smaller creatures are recognized as such in TaleSpire which may be important in some TaleSpire plugins
such as ruleset plugins which may base some game mechanics on the creature size.

When creating an asset that is larger or smaller, you can set the size factor in the info.txt file using
the "size" property. This property defaults to 1 if not specified. The number indiates how many tiles
along the side each creature takes up. A vlaue of 2 means the creature takes up an area of 2x2 (4 tiles).
A value of 3 means the creature takes up an area of 3x3 (9 tiles) and so on. A value of 0.5 means the
creature takes up less than a 1x1 tile.

Within the base size group, the mini should be sized according to its size in realation to the core
TS mini races. For example, dwarves should be shorter than humans and humans should be shorter than
goliaths.

Please note that this function is not yet implemented by the Extra Asset Library (EAL) as this time but
it is already implemented in EAR and passed to (EAL). Thus, as soon as EAL is updated to use this value
all assets with the value set will span at the specified size when added to the board.


## Asset Materials

It is highly recommended that assets be converted to use a single material file. By using a image file for
the various material properties, it is possible to make an asset with seemingly multiple "materials" while
still using only a single asset material.

This not only reduced load time but it also make is more usable with plugins like Retexture which can
change the texture of an asset at runtime but only the main material texture file. It also avoids render
issues where some assets will not show meshes that use a secondary material file. Some assets work perfectly
fine with multiple material files but do not.


## Effects

When creating effects that use Particle System, the effects should either be looping or should end with
a static stage so that, if left undisturbed, the effects persist. This allows effects to be used for both
persistent uses (sphere of flame) and temporary uses (fireball).

Within the info.txt of your effect asset, it is possible to set the "timeToLive" propery which can be set
to a floating point (decimal) number representing the number of seconds that an effect exists for before
it is automatically destroyed. Use this property (as opposed to making the effect end) to indicated that
the effects is *intended* to be temporary. In this way, the intention is clear but the user can override
that using modifiers when the effect is selected from the library.


## Library Groups

The Extra Asset Registration (EAR) plugin (powered by Hollo's Extra Asset Library) allow custom assets to
be placed in custom folders in the library. EAR has settings to turn this feature off completely or to limit
it to a specified list of group names. When ever possible, place custom assets in existing core TaleSpire
groups. If your asset really does not fit one of the core TS categories, create a new categroy such that
it is likely to get a lot of use (i.e. likely to be used by other content creator too). Don't make the new
category to specific, otherwise we will end up with many categories and only a couple assets in each one.
As a rule of thumb: If you don't think a category will get more than 5 assets in it, try to come up with a
more broad name for the categroy which can include more assets.

Do not create categories based on the creator name, date or other restrictive category names.


## Plugins On Main Page

Due to the large number of available plugins and the fact that many of these plugins use dependency plugins,
the following convention is suggested for displaying a plugin name on the main page:

If the plugin provides the user with some direct feature or modifies an core function then display the name
on the main page to indicate to the user that the related functionality is enabled. If the plugin does not
provide any direct user functionality or functionality change (typically meaning the plugin is a dependency
plugin) then the plugin name should not be displayed on the main page. Basically if a plugin is active but
there is no change in functionality unless another plugin is loaded that uses it, the don't display the
plugin name on the main page.

Example: Extra Asset Registration provides the user with the library selection options and implements things
like the transformation, aura, effect and audio options. It also provides hot keys for animation and audio.
As a result this plugin is listed on the main page even though the Extra Asset Library plugin does a lot of
the actual work. The Extra Asset Library, on the other hand, is not listed because on its own it does not do
anything. It needs a plugin like EAR to make use of it in order to provide the functionality to the user.

This may seem unfair to the developers of dependency plugins but this convention has been recommended for two
reasons: 1) to limit the number of plugins that appear on the front page and 2) to only lists the plugins that
a user is interested in. For example, the user does not care about the File Access Plugin, Radial UI plugin
and/or the Stat Messaging plugin plugin. The user cares about plugins like EAR, CMP, Icons, Hide Volume and
so on which actually provide him/her with additional functionality.


## Asset Bundle Building: Info.txt and Portrait.PNG

When creating assets while it is not necessary to include a info.txt and/or portrait.png file, it is highly
recommended. Inclduing these will give your asset more user friendly value because it means that the asset
can be placed in the correct group in the library and it will show up with a custom image icon instea of the
default sad face. The details of the info.txt file format can be obtained in the Extra Asset Registration
plugin documentation (https://talespire.thunderstore.io/package/LordAshes/ExtraAssetsRegistrationPlugin/).


## Asset Bundle Building: Low-res And Hi-res Assets

If you are planning to create either high resolution assets or animated assets consider providing two
versions of the asset in the same assetBundle. Make the first version of the asset with a poly count
between 5k and 12k and remove any animations. If the mesh comes with animations then just remove then
from the animation tab. Name the prefab using the desired name (also the name of the assetBundle). Do not
use underscores in the name since they can cause issues. Next create a second prefab with the desired
higher poly count and/or with animations. Save this prefab in the same assetBundle but with the name
appended with ```high```. For example, laWizard01 and lkWizard01high. Future versions of EAR will have
as setting which will allow users to select the low CPU/GPU assets (when the device is not so powerful)
or the high CPU/GPU assets (when the device is sufficiently powerful).

Do not use _ or other special characters in the name since they can produce issues with features such
as animation and/or sound.

## Asset Bundle Building: Animating Assets

Any animates assets should follow the ```high``` naming convention even if this is the only version of
the asset that the asset bundle is providing. This is important so that possible future plugins can
determine which asset bundles are high performance only.

The latest version of EAR does not require hot key animations to be named Anim01, Anim02, ..., Anim07.
Instead the hot keys just trigger the first thru seventh animation. However, this does not always match
the order in which the animations have been listed in Unity. As such plugins cannot rely on the order
to determine which animation is which. To maximize the compatibility of an asset with future ruleset
it is recommended to include the following animations with the following names. This will allow plugins
to search for those names to see if a asset supports them:

```
Idle = A static pose or animation representing the default character pose or animation.
Ready = An alert of battle stance pose or animation used in combat (or other alert situations).
Melee = A melee attack animation. Plays once.
Range = A range attack animation. Plays once.
Magic = A magic attack animation. Plays once.
Death = A falling over animation. Clamped in last frame.
```

All of these animations are optional but if present using the indicated name will ensure that plugins
can automatically make use of the animations. Obviously the asset can include any number of additional
animations either triggered by the hot keys and/or triggered by the play anmation option and entering
the animation name.