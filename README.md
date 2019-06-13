# Morrighan

Morrighan acts as a kind of proxy, it makes the client connect to a special local server that forwards all packets from the client to the actual server. This way it's able to read every single packet that gets sent or received. These packets can then be passed to other applications, so they can work with them, e.g. loggers like [MabiPale2](https://github.com/exectails/MabiPale2).

## How to log packets

Let's assume you want to log packets from NA. Instead of launching the client through the patcher, you would create a link/bat, like you would to connect to a local server, but with the NA IPs. And instead of client.exe you would use Morrighan.exe (which you have to put into your Mabi folder), that's it.

`Morrighan.exe code:1622 ver:143 logip:35.162.171.43 logport:11000 chatip:54.214.176.167 chatport:8002 setting:"file://data/features.xml=Regular, USA"`

What will happen here is that Morrighan reads the parameters, replaces the logip and port with the ones to a new, invisible local server it started, and finally starts the client. You will see a little window in the upper left, to let you know that Morrighan is running. Once you see that window, you can use a tool like Pale to connect to it and log packets.

The window closes automatically when the client gets closed. You can also double click it to quickly close Morrighan and the client.

## How to connect to Morrighan

Morrighan uses the same API as the tool it was inspired by, "Alissa". It uses WM_COPY messages to communicate between Morrighan's and the subscriber's window. To subscribe to Morrighan, to receive packets, you send the "op" (dwData) `100` to Morrighan's window (window name: "mod_Alissa"), to unsubscribe, you send `101`. While you're subscribed, you receive all incoming (op `0x10101012`) and outgoing (op `0x10101011`) packets via the same method.

For an actual example on how this works, I suggest looking at the corrosponding functions in [Pale](https://github.com/exectails/MabiPale2/blob/master/MabiPale2/FrmMain.cs#L577). Alternatively you can also create a plug-in for Pale, which will be easier.

## Nexon Launcher

With the removal of direct launch in NA and possibly other regions, the NX hash login has to be used to start Morrighan for officials now, which uses the /P parameter to pass the login information to the client directly. Morrighan can assist you in retrieving that parameter, so you can still easily start the client with it.

Starting with Morrighan 1.5.11 you can add the parameter `nxlauncher` to your normal NA start up parameters. If you do so, Morrighan temporarily replaces your Client.exe with itself. Then you click Play in the Nexon Launcher, which doesn't start the client, but Morrighan instead, which now doesn't start the game, but just notes down the NX hash. Afterwards you click OK in the window of the original Morrighan, which reverts the Client.exe back to normal, retrieves the hash from a temporary file, and then starts the client as it normally would.

Example: `Morrighan.exe code:1622 ver:143 logip:35.162.171.43 logport:11000 chatip:54.214.176.167 chatport:8002 setting:"file://data/features.xml=Regular, USA" nxlauncher`

## G13

If we you want to use Morrighan with G13 servers, simply add another parameter, "jpG13".

Example: `Morrighan.exe code:1622 ver:143 logip:127.0.0.1 logport:11000 chatip:127.0.0.1 chatport:8002 setting:"file://data/features.xml=Regular, Japan" jpG13`

## Hiding Morrighan

To hide the Morrighan window you can either click its tray icon to minimize it there, or start Morrighan with the parameter "hideonstart".

## Restrictions

Morrighan only supports the Login and Channel servers, you won't get any messenger packets, it lets the client connect directly there.
