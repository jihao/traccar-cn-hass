# traccar_cn

[![GitHub Release][releases-shield]][releases]
[![GitHub Activity][commits-shield]][commits]
[![custom_updater][customupdaterbadge]][customupdater]
[![License][license-shield]](LICENSE)


_Component to integrate with [traccar_cn][traccar_cn]._

此组件修改官方traccar组件，增加了对火星坐标的转换，具体来说是将GCJ02(火星坐标系)转GPS84。


## 为什么？

在使用traccar server时，国内用户一般换成高德地图才能有更好的体验，但换了地图，默认定位位置反馈显示会有偏差，通过某些转换方法变成火星坐标（有人用Node-RED 或 我的修改版），这样在traccar上的定位偏差问题就解决了。

上述问题解决之后，配置device_tracker将traccar接入HomeAssistant，然而HomeAssistant里面默认用的是OpenStreetMap地图，traccar经上述修改反馈坐标是火星坐标，本traccar_cn组件的目的就是，再将火星坐标转换成GPS84坐标，这样在hass里的显示就可以正常了，继而才能触发状态变化事件。

另外百度地图暂不支持~ 此组件只能与在traccar服务器配置的高德地图配套使用

## 使用流程
1. 安装traccar服务端，配置高德地图，转换成火星坐标系，将自己的设备连入
2. 安装traccar_cn组件，正常配置即可

Traccar 高德地图 演示

Custom Map: https://webrd01.is.autonavi.com/appmaptile?lang=zh_cn&size=1&scale=1&style=8&x={x}&y={y}&z={z}

![example][exampleimg]

**This component will set up the following platforms.**

Platform | Description
-- | --
`device_tracker` |  traccar_cn 组件.

## Installation

**HACS**

**custom_updater**
```yaml
custom_updater:
  track:
    - components
  component_urls:
    - https://raw.githubusercontent.com/jihao/traccar-cn-hass/master/traccar_cn.json
    - ...
```

**手工安装** 
1. Using the tool of choice open the directory (folder) for your HA configuration (where you find `configuration.yaml`).
2. If you do not have a `custom_components` directory (folder) there, you need to create it.
3. In the `custom_components` directory (folder) create a new folder called `traccar_cn`.
4. Download _all_ the files from the `custom_components/traccar_cn/` directory (folder) in this repository.
5. Place the files you downloaded in the new directory (folder) you created.
6. Add `traccar_cn` to your HA configuration.

Using your HA configuration directory (folder) as a starting point you should now also have this:

```text
custom_components/traccar_cn/__init__.py
custom_components/traccar_cn/device_tracker.py
custom_components/traccar_cn/const.py
custom_components/traccar_cn/helper.py
```

## Example configuration.yaml

```yaml
device_tracker:
  - platform: traccar_cn
    host: demo.traccar.cn
    port: 8082
    username: demo
    password: demo
```

## Configuration options

[官方组件配置](trackcar)

支持traccar组件的完整配置，traccar_cn修改版仅增加了火星坐标转换


Key | Type | Required | Default | Description
-- | -- | -- | -- | --
`host` | `string` | `True` | None | traccar 服务器
`port` | `string` | `False` | 8082 | 端口
`username` | `string` | `False` | None | 用户名
`password` | `string` | `False` | None | 密码


## Contributions are welcome!

If you want to contribute to this please read the [Contribution guidelines](CONTRIBUTING.md)

***

[traccar]: https://www.home-assistant.io/components/traccar/
[traccar_cn]: http://demo.trackcar.cn
[commits-shield]: https://img.shields.io/github/commit-activity/y/jihao/traccar-cn-hass.svg?style=for-the-badge
[commits]: https://github.com/jihao/traccar-cn-hass/commits/master
[customupdater]: https://github.com/custom-components/custom_updater
[customupdaterbadge]: https://img.shields.io/badge/custom__updater-true-success.svg?style=for-the-badge

[exampleimg]: example.png
[license-shield]: https://img.shields.io/github/license/jihao/traccar-cn-hass.svg?style=for-the-badge
[maintenance-shield]: https://img.shields.io/badge/maintainer-Joakim%20Sørensen%20%40ludeeus-blue.svg?style=for-the-badge
[releases-shield]: https://img.shields.io/github/release/jihao/traccar-cn-hass.svg?style=for-the-badge
[releases]: https://github.com/jihao/traccar-cn-hass/releases
