# Advanced Server Security Guide
An advanced guide for protect your minecraft server or network.

## Index
- [1. Introduction](#introduction)
  - [What is this guide for?](#what-is-this-guide-for)
  - [Why do I need to secure my server?](#why-do-I-need-to-secure-my-server)
  - [What I need?](#what-i-need)
  - [Disclaimer](#disclaimer)
- [2. Bungeecord](#bungeecord)
  - [Default configuration](#default-configuration)
  - [Authentication plugin](#authentication-plugin)
  - [What plugins should i not use](#what-plugins-should-i-not-use)
  - [Block Invalid Packets](#block-invalid-packets)
  - [Block Exploits](#block-exploits)
  - [Block Bots](#block-bots)
  - [World Downloader](#world-downloader)
  - [Block Commands](#block-commands)
  - [Host Limiter](#host-limiter)
  - [Premium Mode](#premium-mode)
  - [Bungee Authme](#bungee-authme)
  - [Hide Plugins](#hide-plugins)
  - [Summary](#summary)
- [3. Spigot](#spigot)
  - [Block Spigot Exploits](#block-spigot-exploits)
  - [Block OP](#block-op)
  - [IP Based Protection](#ip-based-protection)
  - [Cracked Authentication](#cracked-authentication)
  - [WorldEdit Crash](#worldedit-crash)
  - [For Creative Servers](#for-creative-servers)
  - [Block Items Duplication](#block-items-duplication)
  - [KickAll Exploit](#kickall-exploits)
  - [UUID Spoof](#uuid-spoof)
  - [Custom Payload Exploit](#custon-payload-exploit)
  - [Bot Protection for Spigot](#bot-protecion-for-spigot)
  - [Hide Plugins in Spigot](#hide-plugins-in-spigot)
  - [2nd Check for Staff](#2nd-check-for-staff)
  - [IPWhitelist](#ipwhitelist)
  - [Book Exploit](#book-exploit)
  - [Bad Potion Exploit](#bad-potion-exploit)
  - [Skull Exploit](#skull-exploit)
  - [Spigot Summary](#spigot-summary)
- [4. Extra](#extra)
  - [Firewall](#firewall)
  - [IP Forward](#ip-forward)
  - [Hide spigot ports](#hide-spigot-port)

![Introduction](http://i.imgur.com/Ih40NJz.png)
###### Introduction
### What is this guide for?
This guide is created with the sole purpose of protecting our server against exploit abuse that could damage the server or network.  
With this guide you can block most exploits and bugs that the Grieffers (A.K.A Skiddies) use to break our cubes.  

### Why do I need to secure my server?
If you search on Google "Grief minecraft server" this will give you enough reason to protect your server, in summary you run the risk that your account is compromised or that hacked clients can attack your vulnerable minecraft server/network.  

### What I need?
You don't need much knowledge, try to know at least: how plugins are installed, how they are configured, how ports work, how servers and packets work. Also to improve security I recommend not using host pages, use a VPS or Dedicated (Best option)

### Disclaimer
It is impossible to block all exploits, most of the grief is due to the stupidity of the owners, administrators or who has made a patent configuration of the server as the fact of using plugins with bypasses or configuring them incorectly.  
Nor do I promise you that your network/server will be completely inescapable, nor will I be responsible for any damage you do to your server with this guide. (If you follow everything to the letter nothing bad will happen)  
  
![BungeecordBanner](http://i.imgur.com/HyNnNGE.png)  
##### Bungeecord
If you don't use bungeecord (which one you should use) you can skip this part even though I don't recommend it at all.  

### Default configuration
The bungeecord server already comes with a default configuration that helps users understand how it works, but it is dangerous to leave some parameters as they are.  
```yaml
# Leaving this is quite dangerous.
groups:
  md_5:
  - admin

# change them to how they are continuing
groups:
  md_5: []

# make sure that the following values are as follows.
ip_forward: true
prevent_proxy_connections: true

# This only if your server has support for non-premium users or if you want users to enter the lobby to forcefully enter.
listeners:
  force_default_server: true
```

### Authentication plugin
Never use auth plugins in the bungeecord, it may sound safe but it can be exploited in many ways, it is best to have a dedicated auth server, in case of using multiple lobbies use a MySQL connection. Also do not use AuthmeBridgeBungee and if you are not going to listen to this point and you will still place an Auth plugin in the bungee, at least use [DynamicBungeeAuth](https://www.spigotmc.org/resources/dynamicbungeeauth-premium-command-semi-premium-system-sessions.27480) that of all of the market, is the one that is best programmed in my opinion.

Example of exploit: 
if you are kicked from the spigot instance but the bungeecord does not eject your currentServer variable it could be null giving you the opportunity to bypass functions locked on the auth server. As an example changepassword or unregister (It happens when you send packets to the spigot server that this closes your connection instantly in an insecure way which the bungeecord fails to detect)

### What plugins should i not use
It is advisable to have the minimum possible plugins in the Bungeecord instance, even so avoid placing this type of plugins:
1. Global report system (Like any "/report" plugin)
2. Global moderation system (Like Litebans)
3. Global message system or staff chat
4. Permissions plugins for bungeecord (Like BungeePerms)
5. Any authentication plugin (Like BungeeAuth)
6. Viaversion (Use Flamecord or Travertine)
7. Any antivpn/proxy system.

### Block Invalid Packets
To protect our server from attacks of invalid exploits and packages, it is advisable to use Flamecord (Flamecord is a proxy software, travertine fork that mitigates exploit attacks) [download it here](https://2l-studios.com/flamecord/).

### Block exploits
we can secure our spigot servers from the bungeecord instance with some useful plugins, [ExploitFixer](https://www.spigotmc.org/resources/2ls-exploitfixer-professional-server-antiexploit.62842/) is the most recommended (and it's free)

### Block bots
The most advisable thing is to block bots in the instancai bungeecord, for this we will use the following [Antibot plugin](https://www.spigotmc.org/resources/2ls-antibot-the-ultimate-antibot-plugin.62847/).  
  
Remember that bot attacks cause a waste of resources on your server that can crashe it.

### World Downloader
To prevent users from downloading our server constructions using WorldDownloaderMod, we will use this [plugin](https://www.spigotmc.org/resources/antiworlddownloader-bungee.37106/) that blocks that mod.

### Block Commands
Here is a way to block global commands on our server, this can be very useful to disable commands that can compromise server security.  
for this we will use a plugin calle [BungeeCommandBlock](https://www.spigotmc.org/resources/bungee-command-block.5935/)

### Host Limiter
Although it is not very useful but it can be if you put it to good use, you can block from which domain each user must enter or allow only 1 for all. Those who open the door to create a domain system for each staff on the server.  
for this we will use a plugin calle [BungeeHostLimiter](https://www.spigotmc.org/resources/bungeehostlimiter.13036/)

### Premium mode
It is not recommended since there have been cases of servers which this plugin has been bypassed but in the networks that I saw that they had it, these cases were not reported, and although it is not recommended if you had to choose a plugin in a premium way, I would choose [FastLogin](https://www.spigotmc.org/resources/srlegsinis-fast-login-login-made-faster-and-easier.53222/)

### Bungee Authme
Not to be confused with BungeeAuthmeBridge (this plugin is garbage), the following plugin is official from Authme developers and simply blocks the actions sent to the bungee by users who have not logged in. (Commands, messages, etc.)  

Warning: It could cause incompatibility with premium authentication plugins.  
Plugin: [AuthmeBungee](https://www.spigotmc.org/resources/authmebungee.50219/)

### Hide Plugins
To prevent users from observing the server plugins using the TabComplete method, we can use the plugin called: [CanelaAntiPluginSteal] (https://www.spigotmc.org/resources/canela-anti-pluginsteal.1150/)

### Summary
The truth is not necessary to follow all these steps except for [Block Bots](#block-bots), [Block Exploits](#block-exploits) and Block [Block Invalid Packets](#block-invalid-packets). While everything is in order it should not be why there are exploits in the bungeecord.

![Spigot](http://i.imgur.com/SUHpEno.png)
###### Spigot

### Block Spigot Exploits
As in bungee, we must protect our Spigot server from exploit attacks, for this we will use this plugin. [Exploitfixer](https://www.spigotmc.org/resources/2ls-exploitfixer-advanced-server-anticrash.62842/) works for both Spigot and bungeecord, it is advisable to have it in both instances since there are exploits for spigot that bungee is unable to detect.

### Block OP
It is highly recommended to block the OP and not give it to anyone, not even have it ourselves. To block that a user can obtain OP thanks to a permit or by another operator, we will use [Anti ForceOP](https://dev.bukkit.org/projects/anti-forceop).  
You can also configure that operators do not have any type of permissions by changing this parameter in the spigot server configuration:
```properties
op-permission-level=0
```
Default value: 4  
Recommended value: 0

### IP Based Protection
If you want one more layer of protection, you can protect the accounts of all staff using [AccountGuard](https://dev.bukkit.org/projects/accountguard). This plugin allows you to restrict the IP address from which you can access an account. In this way you can protect your account or those of the staff so that they can only be accessed from their respective IP address.

### Cracked Authentication
If your server supports non-premium players, you must have an authentication plugin, otherwise your server will be compromised to hacked clients. For this you can use a plugin below:  
[Authme Reloaded](https://www.spigotmc.org/resources/authmereloaded.6269/) (Recommended).  
[Login Security](https://www.spigotmc.org/resources/loginsecurity.19362/).  

### WorldEdit Crash
There are several exploits when using worldedit that can crash the server besides that this plugin uses many resources and its tasks are Sync (that is, that the users will suffer from lag and the server will be frozen while this plugin is working) to correct this we will use [FastAsyncWorldEdit](https://www.spigotmc.org/resources/fast-async-worldedit-voxelsniper.13932/)

### For Creative Servers
There are several hacked clients capable of generating malicious, corrupt items or with custom NBT tags that can range from crashing to the server to taking huge enchantments.  
For this we will use [ExploitFixer](https://www.spigotmc.org/resources/2ls-exploitfixer-advanced-server-anticrash.62842/) and/or [ItemFixer](https://www.spigotmc.org/resources/itemfixer-remove-creative-hacked-items-from-your-server.34250/).

### Block Items Duplication
By default the minecraft code has some bugs that allow duplicate objects in the chests taking advantage of certain bugs, to solve this you can use a plugin below:  
[ExploitFixer](https://www.spigotmc.org/resources/2ls-exploitfixer-advanced-server-anticrash.62842/) (Recommended).  
[Dupe Fixes](https://www.spigotmc.org/resources/dupe-fixes-illegal-stack-remover.44411/) (Dedicated plugins just for Dupe Exploits).  
[Confiscate](https://www.spigotmc.org/resources/%E2%98%85-confiscate%E2%84%A2-hacks-exploits-bad-staff-protection-1-7-10-1-15-1.37893/) (Premium and excellent option with some usefull functions!!)

### KickAll Exploit
Normally in minecraft when you enter the server and your account is already online, it is disconnected giving way to the most recent connection, authme and bungeecord solve this but if your server is a network and you choose to use ipwhitelist since you can not install a software firewall then your server is vulnerable to an exploit that matches for each online player, making a connection which kicks the selected player (kicking all players)

To solve this we will use the plugin called [AntiUserSteal](https://www.spigotmc.org/resources/antiusersteal.11986/)

### UUID Spoof
Hacked clients can easily change their uuid, which imposes a great risk for servers without adequate protection, luckily there are several plugins that solve this, for example [ExploitFixer](https://www.spigotmc.org/resources/2ls-exploitfixer-advanced-server-anticrash.62842/) and [AntiUUIDSpoof](https://www.spigotmc.org/resources/security-antiuuidspoof.33721/) (Recommended for mixed-mode).

### Custom Payload Exploit
CustomPayload packets are called packages that are sent to the server with a specific parameter, these packages are mostly used for communication between the client and the server in some mods or for communication between spigot/bungeecord.  
Sending such large-scale packets or packets that the server cannot process can crash the server if it does not have adequate protection.  
  
To solve this we can use [ExploitFixer](https://www.spigotmc.org/resources/2ls-exploitfixer-advanced-server-anticrash.62842/) or [CustomPayloadFixer](https://www.spigotmc.org/resources/custompayloadfixer-bungeecord-bukkit-spigot.39891/).

### Bot Protection for Spigot
If you do not have a bungeecord instance then the plugin mentioned in [Block bots](#block-bots) will not work for you, here is a list of antibot plugins which could be useful:  
[AntiBot-Ultra](https://www.spigotmc.org/resources/antibot-ultra.45024/).  
[AntiBot-Attack](https://www.spigotmc.org/resources/anti-bot-attack.18540/).

Remember that bot attacks cause a waste of resources on your server that can crash it.

### Hide Plugins in Spigot
If you do not have a bungeecord instance then the plugin mentioned in [Hide Plugins](#hide-plugins) will not work for you, to block users from seeing your plugins you can use [PLSecure](https://www.spigotmc.org/resources/plsecure.7615/),

### 2nd Check for Staff
If you want to have a second authentication for your administrative staff then you can opt for this plugin.  
[PinProtect](https://www.spigotmc.org/resources/pinprotect.34626/) adds a second authentication in the form of a pin in case the password is bypassed. (It is advisable to place it in the lobby)

### IPWhitelist
It is highly recommended that you have a firewall software on the server system, but if you do not have access to a terminal either because you use a web page that offers a host for minecraft servers or for any other reason and you have a Network, then you must use [IPWhitelist](https://www.spigotmc.org/resources/ipwhitelist.61/).  
  
[IPWhitelist](https://www.spigotmc.org/resources/ipwhitelist.61/) restricts from which bungeecord your Spigot server can be accessed.  
otherwise the door is open to which they can access with any username if they discover the port of your Spigot server.

### Book Exploit
There are hacked clients able to create books with almost infinite enchantments. These books when interacting with a user cause the server to have to process a lot of information causing a memory overflow and causing it to close.  
To fix this we can use [Book-Sign Exploit Fix](https://www.spigotmc.org/resources/book-sign-exploit-fix-book-and-quil-with-all-enchants-level-32767.45954/) or [ExploitFixer](https://www.spigotmc.org/resources/2ls-exploitfixer-advanced-server-anticrash.62842/).

### Bad Potion Exploit
as well as hacked books, the same thing happens with potions, [AntiHackedPotions](https://www.spigotmc.org/resources/antihackedpotions.17716/) or [ExploitFixer](https://www.spigotmc.org/resources/2ls-exploitfixer-advanced-server-anticrash.62842/), those plugins detects potions with dangerously high spells or that can get the server crashed and removes them.

### Skull Exploit
Like the previous points, minecraft heads have many properties that can be exploited and corrupt worlds, chunks or crash the server. We can detect and remove them using [Skull Exploit Fix](https://www.spigotmc.org/resources/skull-exploit-fix.26099/) or [ExploitFixer](https://www.spigotmc.org/resources/2ls-exploitfixer-advanced-server-anticrash.62842/).

### Spigot Summary
the truth is that most exploits are covered by [ExploitFixer](https://www.spigotmc.org/resources/2ls-exploitfixer-advanced-server-anticrash.62842/), but do not overlook AntiBot protection and some points that [ExploitFixer](https://www.spigotmc.org/resources/2ls-exploitfixer-advanced-server-anticrash.62842/) still does not solve.

![Extra](http://i.imgur.com/deqw3at.png)
###### Extra

### Hide spigot port
The most advisable thing is to use a firewall to block the ports of the spigot servers from ips that do not come from the local network (127.0.0.1) but making spigot only listen to the local IP (127.0.0.1) is a good practice that NEVER forget.  

```yaml
# On spigot servers (server.properties)
server-ip= 127.0.0.1
```
```yaml
# On bungeecord instance (config.yml)
# in any server in the "servers" list:
servers:
  server-1:
    address: 127.0.0.1:xxxxx
    restricted: false
  server-2:
    address: 127.0.0.1:xxxxx
    restricted: false
  server-3:
    address: 127.0.0.1:xxxxx
    restricted: false
```

### IP Forward
if the bungeecord hook or ip forward are deactivated then the spigot servers will be unable to recognize the IP address of the users.  
  
For this we will place the ip_forward option in the bungeecord config.yml to true, and the "bungeecord" option in the spigot.yml file of all spigot servers to true.

```yaml
# Config.yml of Bungeecord
ip_forward: true
```

```yaml
# Spigot.yml of each spigot server
settings:
  bungeecord: true
```

### Firewall
A firewall is a software that allows us to restrict incoming and outgoing connections to the server, it is extremely recommended to use [IPTables](https://www.digitalocean.com/community/tutorials/iptables-essentials-common-firewall-rules-and-commands) or [UFW](https://www.tecmint.com/setup-ufw-firewall-on-ubuntu-and-debian/).

You can get more information searching on the internet.

# The END
###### Made with ❤️ Need help? contact me on discord (view my github profile) or contact me on twitter: [@Sammwy_](https://twitter.com/sammwy_)
