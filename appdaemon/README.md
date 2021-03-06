This appdaemon app allows rgb lights to be synced with the thumbnail of a media player in Home Assistant.

# Configuration

## appdaemon.yaml

Create a file name `secrets.yaml` alongside the `appdaemon.yaml` file with this content:

```
token: <a_long_lived_token_from_home_assistant>
ha_url: <home_assistant_url>
```

## app.yaml

| Property        | Description                                                                                                                                                                        |
|-----------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| media_player    | The media player to sync.                                                                                                                                                          |
| photo_attribute | [_Optional, defaults to `"photo_attribute`_] The photo attribue to listen for change.                                                                                                                                           |
| condition       | [_Optional_], If not null, it must contain `entity` and `state` properties. Change the color of the lights only if the entity has the specific state.                                                  |
| lights          | A list of all the lights to be synced with the media_player. A color palette from the thumbnail image is calculated, assigning a different color for each light. |


# Installation

https://appdaemon.readthedocs.io/en/latest/INSTALL.html

Clone this folder into `/home/pi/appdaemon`

## Appdaemon

```
$ python3 -m venv appdaemon_env
$ source appdaemon_env/bin/activate
$ sudo apt-get install libtiff5-dev zlib1g-dev libfreetype6-dev liblcms2-dev libwebp-dev libharfbuzz-dev libfribidi-dev tcl8.6-dev tk8.6-dev python-tk libopenjp2-7
$ pip3 install appdaemon Pillow
$ sudo chown -R pi:pi /home/pi/appdaemon
```

## Start at reboot

```
$ cp appdaemon@appdaemon.service /etc/systemd/system/appdaemon@appdaemon.service
$ sudo systemctl daemon-reload
$ sudo systemctl enable appdaemon@appdaemon.service --now
```

# Testing

You can test that the app is working like so:

```
(appdaemon_env) pi@hassbian:~/appdaemon $ python3 -m appdaemon.admain -c "/home/pi/appdaemon/conf/"
```

# Log

```
$ sudo journalctl -u appdaemon@appdaemon.service -f
```