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

### Block Exploits
As in bungee, we must protect our Spigot server from exploit attacks, for this we will use this plugin. [Exploitfixer](https://www.spigotmc.org/resources/2ls-exploitfixer-advanced-server-anticrash.62842/) works for both Spigot and bungeecord, it is advisable to have it in both instances since there are exploits for spigot that bungee is unable to detect.

### Block OP
It is highly recommended to block the OP and not give it to anyone, not even have it ourselves. To block that a user can obtain OP thanks to a permit or by another operator, we will use [Anti ForceOP](https://dev.bukkit.org/projects/anti-forceop).  
You can also configure that operators do not have any type of permissions by changing this parameter in the spigot server configuration:
```properties
op-permission-level=0
```
Default value: 4  
Recommended value: 0
