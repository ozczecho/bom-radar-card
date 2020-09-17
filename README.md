# BOM Radar Card

A rain radar card using the new tiled images from the Australian BOM

[![GitHub Release][releases-shield]][releases]
[![License][license-shield]](LICENSE.md)
[![hacs_badge](https://img.shields.io/badge/HACS-Custom-orange.svg?style=for-the-badge)](https://github.com/custom-components/hacs)

## Support

Hey dude! Help me out for a couple of :beers: or a :coffee:!

[![coffee](https://www.buymeacoffee.com/assets/img/custom_images/black_img.png)](https://www.buymeacoffee.com/theOzzieRat)

## Description

The new Austalian BOM radar products (mobile app and https://weather.bom.gov.au/) now use map tiles to distribute the radar images. This allow for one continous map that can be zoomed and panned seamlessly. This card allows this to be displayed within Home Assistant. The one drawback of the new system is that currently the BOM only publishes new tiles every 10 minutes (compared to 6 minutes with the old radar products) and there is a bigger lag in them being published. This results in the most recent radar image being between 10 to 20 minutes old at any point in time. The upside is that the radar tiles are available for a much longer time frame. This means you can create radar loops of up to at least 24 hours.

![BOM Radar card](https://raw.githubusercontent.com/theOzzieRat/bom-radar-card/master/bom-radar-card.gif)

## Options

| Name             | Type    | Requirement  | Description                                   | Default                         |
| ---------------- | ------- | ------------ | --------------------------------------------- | ------------------------------- |
| type             | string  | **Required** |                                               | must be `custom:bom-radar-card` |
| center_latitude  | number  | **Optional** | The initial center latitude of the map        | `-27.85`                        |
| center_longitude | number  | **Optional** | The initial center longitude of the map       | `133.75`                        |
| zoom_level       | number  | **Optional** | The initial zoom level, can be from 4 to 10   | `4`                             |
| frame_delay      | number  | **Optional** | The number of milliseconds to show each frame | `500`                           |
| frame_count      | number  | **Optional** | The number of frames to use in the loop       | `10`                            |
| show_marker      | boolean | **Optional** | Show the home icon at the marker position     | `false`                         |
| marker_latitude  | number  | **Optional** | The latitude for the home icon if enabled     | the same as center_latitude     |
| marker_longitude | number  | **Optional** | The longitude for the home icon if enabled    | the same as center_longitude    |
| show_range       | boolean | **Optional** | Show range rings around marker position       | `false`                         |
| show_scale       | boolean | **Optional** | Show a scale in the bottom left corner        | `false`                         |
| extra_labels     | boolean | **Optional** | Show more town labels (labels become smaller) | `false`                         |
| map_style        | string  | **Optional** | Specifies the style for the map               | `'light'`                       |

### Map style

Specifies the style of map to use. Valid values are 'light', 'dark' and 'voyager'. These are based off the Carto map styles that are available.

## Samples

This is the configuration used to generate the radar loop on this page.

```yaml
type: 'custom:bom-radar-card'
frame_count: 10
center_latitude: '-25.567607'
center_longitude: '152.930597'
marker_latitude: '-26.175328'
marker_longitude: '152.653189'
show_marker: true
show_range: true
zoom_level: '8'
```

This will display a radar for the whole of Australia showing the previous 24 hours of radar images with a 100mSec delay between frames.

```yaml
type: 'custom:bom-radar-card'
frame_count: 144
frame_delay: 100
marker_latitude: '-33.857058'
marker_longitude: '151.215179'
show_marker: true
show_range: false
```

## ToDo

These are some things that are left to do.

- Finish adding the various options to the Lovelace gui editor (I got stuck with how to add toggle buttons for the boolean options)
- Add more options to disable the controls
- Add a km scale at the bottom left
- Allow customisation of ring sizes (possibly add text to show the size)
- Make it mobile friendly

## Install

If you use HACS, the resources will automatically be configured with the needed file.

If you don't use HACS, you can download js file from [latest releases](https://github.com/theOzzieRat/bom-radar-card/releases). Drop it then in `www` folder in your `config` directory. Next add the following entry in lovelace configuration:

```yaml
resources:
  - url: /local/bom-radar-card.js
    type: module
```

[license-shield]: https://img.shields.io/github/license/theOzzieRat/bom-radar-card.svg?style=for-the-badge
[releases-shield]: https://img.shields.io/github/release/theOzzieRat/bom-radar-card.svg?style=for-the-badge
[releases]: https://github.com/theOzzieRat/bom-radar-card/releases
