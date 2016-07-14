---
layout: default
---
## Why?
{:.no_toc}

Firefox's recent direction have been away from functionality for advanced users and more towards removing features and functionality to appeal to the lowest common denominator. This guide explains a sane set of default plugins and settings that attempt to reverse these changes and return Firefox to its place as a useful tool for everyone, not just your grandparents.

The browser still has a number of umatched features, not least of which is a very rich plugin ecosystem. By leveraging these plugins and making some configuration changes, Firefox can be restored to most of its former glory.

## Philosophy

Despite the annoyance-driven dumping on Firefox, and Mozilla, that you're about to read, you shouldn't get the wrong idea. Firefox is good software, by a great group of people! The fact that every single annoyance I call out here can be solved with either a plugin or configuration tweak is a testament to Firefox's flexibility.

I just think Mozilla has forgotten their roots in an attempt at greater market share, hence some of the ridiculous defaults and changes.

This guide intends to configure Firefox according to the following simple philosophy:

1. The user is the most important person touching the browser.
2. The user is knowledgable and responsible for their own actions.
3. Features or characteristics that are hostile to the user in any way, by misusing their time, attention, data, or control, are unwelcome.
4. The browser's job is to display content from the web, and otherwise be as invisible as possible.

## Contents
{:.no_toc}
* TOC
{:toc}

## <i class="fa fa-gear"></i> Control

### <i class="fa fa-certificate"></i> Addon Signing Override

As of Firefox v43, Mozilla has taken a very paternalistic, nanny-like stance with their users: [You may not install addons](https://wiki.mozilla.org/Addons/Extension_Signing) into Firefox that they have not signed. This is supposedly a way to prevent malicious addons from being installed. What remains unanswered is how malware that can install addons can't mess with the user in other ways.

If you're not all that interested in Mozilla Inc telling you what plugins you can and can't install, you've got a couple options.

Currently, as of writing, the addon checking can be disabled in an advanced configuration option, This setting is planned to be removed in the next major version, so you should not rely on it.

If you want to continue to use your addons, you must either:

* Uninstall and reinstall them from the official Addons site, if the plugin author has done so
* Use a version of Firefox with the check override still enabled

I recommend the second option, especially if you're using plugins not supported by their authors anymore. Specifically, Firefox ESR. It's an "Extended support release" version of Firefox intended for use by organizations who don't move as fast as Mozilla does. Most importantly, ESR releases last for a very long time, which means your plugins will work longer, and you'll be insulated from any further Mozilla fad driven development.

[ESR 45 can be downloaded here](https://www.mozilla.org/en-US/firefox/organizations/all/)

Once installed, you must navigate to `about:config`, and set the `xpinstall.signatures.required` option to `false`.

### <i class="fa fa-file-code-o"></i> Addon Compatibility Checks

For quite some time (I'm unable to even find the version where this was implemented - maybe it's always been there), Firefox will refuse to install addons that have not been updated to support newer versions of the browser. There *used* to be an option in `about:config` to override these checks, but it was uncerimoniously removed for unknown reasons.

Many times, you can override this check, and have an addon work flawlessly.

To reinstate the override, install the [CheckCompatibility](https://addons.mozilla.org/en-US/firefox/addon/checkcompatibility/) addon.

Note that if you still receive messages that an addon you want to install isn't compatible even after installing this and overriding the "this isn't compatible with your version" warning, it means that the addon is really, truly impossible to load on your version of Firefox, and there's nothing that can be done save for upgrading Firefox or the plugin.


### <i class="fa fa-plug"></i> Unwanted Plugins

Mozilla recently bundled two plugins with the browser for various reasons related to their business. Critically, those reasons are not related to your comfort or productivity!

Those would be Hello, a WebRTC-based video chat service, and Pocket, a link storage/sharing tool.

We don't want this garbage, we want a web browser, so let's disable them.

#### Hello

The first step is to remove the icon. Look on your toolbar for a smiley face in a chat bubble. Right click it, and select "remove from toolbar".

Next, navigate to `about:config`, and look for an option named `loop.enabled`. Set this to false, and restart your browser.

Reports exist that this function [likes to come back after being disabled](https://support.mozilla.org/en-US/questions/1048469#answer-705829). So far, toggling the `loop.enabled` option to false stops it again for a while. This is probably update-related.

#### Pocket

Pocket is more of a problem; it apparently was stealth installed [with a security update](https://support.mozilla.org/en-US/questions/1065182#answer-737531). Disabling it is identical to the steps for Hello.

1. Remove the icon
2. Navigate to about:config
3. Toggle `browser.pocket.enabled` to `false`

### <i class="fa fa-money"></i> New page ads

Firefox has officially become adware. Out of the box, accessing the new tab page results in sponsored "tiles" in your face.

To Mozilla's credit, these ads lack the traditional privacy and security concerns (i.e. there's no external data being transmitted), but they are still quite tacky, and most importantly, are for Mozilla's benefit, not yours.

To remove these, bring up the new tab, hit the gear on the top right, and set the option to anything other than "enhanced".

## <i class="fa fa-lock"></i> Security

Firefox's security record is abysmal. So much so that, a popular hacking contest, Pwn2Own, dropped Firefox from its annual competition for being [too easy](https://it.slashdot.org/story/16/02/12/034206/pwn2own-2016-wont-attack-firefox-because-its-too-easy) to take over. Unfortunately, the message Mozilla seems to take from this track record is more like Sony's response to the PS3 being hacked: remove functionality.

With that in mind, I recommend installing a suite of addons to prevent active content from running in the browser unless you specifically authorize it. All the malware in the world can't hurt you if it can't run.

### <i class="fa fa-check-square"></i> Ad Blocking

Ads are a primary vector for malware and *must* be blocked by default. For this, I suggest [uBlock Origin](https://github.com/gorhill/uBlock). (Not to be confused with the addon at ublock.org).

uBlock will kill most advertisements you run across. You can easily whitelist sites you want to see ads on to support their authors, but blocking ads by default is *essential* from a security standpoint.

uBlock will also, with some minor configuration tweaks, block other annoyances on the web, such as social network icons.

### <i class="fa fa-square"></i> Active Content Blocking
Now we need to deal with Flash and other active content. Flash is still useful to have, with many sites still using it, but given its *awful* security record, it should be restricted to sites where you know it needs to run.

You can choose your own level of security here.

* [Flashblock](https://addons.mozilla.org/en-US/firefox/addon/flashblock/) makes all Flash elements click-to-play, which is probably sufficient from a security standpoint.

If you want to go further, we can also make all active content (like Flash, but also including Javascript) be whitelisted before it runs. For this, you can use:

* [Noscript](https://noscript.net/), denies all scripts by default until you explicitly allow them. It can  very annoying for the first week or so you use it (as every site you touch will have to be whitelisted), but you'll be *very* safe from random scripts running on random pages.

We can still go one step further. What if you want to prevent bits of one page from contacting another webpage? For this, you'd use something like:

* [RequestPolicy](https://requestpolicycontinued.github.io/). Much like Noscript, this will immediately break functionality until you've used it long enough and whitelisted what you normally use.

There's a very stark demonstration of the security vs usability principle here. The more you lock your browser down, the more of a pain in the ass it's going to be (at least in the short term).

For a completely casual user, you're fine with Flashblock. More paranoid users with more time to kill can use Noscript or RequestPolicy.

### <i class="fa fa-shield"></i> Encrypted Media Extensions

EME is a browser framework for viewing encrypted media that uses DRM (digital restriction management). After some amount of controversy, Mozilla deployed this framework starting from version 38.

This framework is much like a plugin system. On its own, it does nothing. However, when accessing appropriate content, it facilitates executing a closed source, proprietary blob of code whose job it is to treat you, the user, as hostile.

Furthermore, the browser comes pre loaded with the plugins for Adobe and Google DRM schemes.

Given the nature of these plugins, and the fact that it is impossible to audit their security, **I recommend disabling this system**.

To do so:

1. Navigate to the preferences panel, and select "Content"
2. Remove the check mark next to "Play DRM content".

This will delete the downloaded plugins, stop any further plugins from being downloaded, and disable the EME system entirely.

### <i class="fa fa-unlock"></i> SSL Validation

One problem with SSL as it stands today is that many sites use a configuration that is inherently insecure. Whether that be by using weak certificate signatures or by weak ciphers, it is valuable to know what the security posture of a site is before you begin transmitting sensitive data to it. Just because it uses SSL doesn't mean it's inherently secure.

I recommend installing the [Calomel SSL Validation](https://addons.mozilla.org/en-us/firefox/addon/calomel-ssl-validation/) plugin. It gives you a small shield icon on your address bar. If a connection meets best practices, the icon will be green, and red if it's not up to snuff. Clicking will give you the reason for the grade.

## <i class="fa fa-user"></i> Privacy

There are some out-of-the-box options you should evaluate for yourself.

Generally, from a web privacy standpoint, you want to blend in. You want to look just like every other user that accesses a website. This means taking actions that stand out, like enabling do not track, disabling images, or javascript, serves to identify you *more*. [The EFF has a great site that serves to illustrate this](https://panopticlick.eff.org).

### <i class="fa fa-user-times"></i> Do not track

Enabling do not track (hereafter: DNT) sets a header in your browser requests that informs the remote server that you wish not to be tracked. In other words, it's purely on the honor system, and given that the online advertising industry could be charitably described as a pirhana infested toilet bowl, it's totally ineffective as a countermeasure.

Worse, the option is off by default. Toggling it on means that you are part of a minority of users that have bothered to enable the option - meaning you're drawing attention to yourself and differentiating your traffic.

I recommend **leaving this option disabled**.


### <i class="fa fa-cloud-download"></i> Prefetching

Prefetching preemptively downloads data from links on pages you visit, with the goal of making the browser load the next page quickly should you hit any of the links.

Most of the time, this is a sane performance improvement, and it's common enough on browsers nowadays that it's not strange to see preemptive requests for pages you haven't browsed yet.

**In general, I recommend leaving prefetching enabled.**

You should consider disabling it if:

* You're on a metered internet connection where every byte counts
* You live in a repressive regime where accessing the wrong link could impact your real life

There are multiple kinds of prefetching:

* Link prefetching, where the data is actually downloaded ahead of time based on tagged links on a page.
* DNS prefetching, where the browser will look up the address associated with links.
* Speculative pre-connections, where the browser background downloads:
  * Hovered links on the new tab page
  * Search bar/new tab page search results

To disable all of these:

1. Navigate to `about:config`
2. Set `network.prefetch-next` to `false`
3. Set `network.dns.disablePrefetch` to `true`
4. Set `network.http.speculative-parallel-limit` to `0`

### <i class="fa fa-cubes"></i> Third-Party Content

An average webpage loads content from many different places - Google for fonts, Facebook for social buttons, and so forth. Much of this functionality is benign in nature, but some of it exists to track you across the web. The EFF has released a plugin, called [Privacy Badger](https://addons.mozilla.org/en-US/firefox/addon/privacy-badger-firefox/), that notifies you if the page you're on is leaking your browsing footprint to third parties.

**HOWEVER**: The plugin forces the "do not track" header to be turned on, which as detailed above, you may not want in situations where privacy is vital. Privacy Badger stops day to day tracking of your casual activities, but DNT being enabled may make make your browsing stand out by enabling this rarely used header.

* If you are a casual web user, I recommend installing it.
* If your privacy is absolutely vital to your survival, I recommend passing.

### <i class="fa fa-wifi"></i> Telemetry

Telemetry is anonymized data that Firefox sends back to Mozilla that details, among other things, health stats, UI usage, and so forth.

This will be a controversial stance to take, but **I recommend disabling all telemetry.** Although Mozilla has not shown any inkling that this data is being used to abuse your privacy, I still disable it on my browsers to prevent upstream decisions about how I use my browser from being used against my usability - decisions like "nobody uses feature X, let's remove it".

While it would sound like making your "voice" "heard" by representing your actual usage to Mozilla in these metrics would be a good thing, historically, telemetry data has been used to support things like the awful "Australis" UI redesign, among other changes. I would rather tell Mozilla what features I want, rather than having them measure my clicks to figure it out (and screw it up) on their own.

To disable telemetry, navigate to the "Preferences" menu, select "Advanced", then "Data Choices". Ensure the first two options are disabled.

Crash logs are another matter entirely - choose according to your own preference here. I personally leave those enabled, since crash bugs are objectively harmful to *all* Firefox users.

## <i class="fa fa-map"></i> Usability

The following tweaks are intended to fill some missing gaps in Firefox's feature set, and to revert some of the more newbie friendly, advanced hostile changes made in recent releases.

### <i class="fa fa-flash"></i> Classic UI

The new firefox UI, rolled out in version 29 and code named "Australis" has drawn [no small amount of criticism](http://www.computerworld.com/article/2489336/internet/firefox-ui-revamp-sparks-complaints-searches-for-alternatives.html) due to the new UI looking shockingly like the Chrome browser, the repositioning of UI elements, outright removal of the addon bar, and the reduced overall information density by wasting many more pixels on dead space.

The great majority of these changes, including removal of features like the addon bar, can be rolled back using the [Classic Theme Restorer](https://addons.mozilla.org/en-US/firefox/addon/classicthemerestorer/) plugin.

### <i class="fa fa-file"></i> Tab Management

Built-in Firefox tab management isn't great, especially if you're like me and tend to use Firefox as a brain extension. Once again, there's a plugin to the rescue: [Tab Mix Plus](https://addons.mozilla.org/en-US/firefox/addon/tab-mix-plus/). A particularly useful option in TMP is the ability to stack tabs at the top of the screen and scroll through them vertically like any other content, rather than purely horizontally.

## <i class="fa fa-gavel"></i> Legalese and such

Fix Firefox is an open site. Changes can be proposed, and the source code accessed at the [Github repo.](https://github.com/Karunamon/FixFirefox)

<a rel="license" href="http://creativecommons.org/licenses/by-sa/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-sa/4.0/88x31.png" /></a><br /><span xmlns:dct="http://purl.org/dc/terms/" href="http://purl.org/dc/dcmitype/Text" property="dct:title" rel="dct:type">Fix Firefox</span> by <a xmlns:cc="http://creativecommons.org/ns#" href="https://tkware.info" property="cc:attributionName" rel="cc:attributionURL">Michael Parks</a> is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-sa/4.0/">Creative Commons Attribution-ShareAlike 4.0 International License</a>.

For the lawyers: This site is blatantly not authorized by, endorsed by, or probably even liked by Mozilla Inc, or any other related company. Any trademarks or copyrights used are done so in a descriptive or fair use fashion. If you think for a moment this is an official site, what the *hell* is wrong with you?
