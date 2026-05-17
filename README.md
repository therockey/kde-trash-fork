# KDE Trash Plasmoid (Rockey's version)
This is a fork of the QML version of the KDE Plasma trash widget (**org.kde.plasma.trash**) as featured in Plasma versions **up to (and including) 6.5**. 

This repo is maintained because starting with Plasma release 6.5, all system-wide widgets are being progressively ported from QML to **compiled QML** (read more about it [here](https://blog.davidedmundson.co.uk/blog/a-roadmap-for-a-modern-plasma-login-manager/) and [here](https://old.reddit.com/r/kde/comments/1ohnsc7/plasma_65_weather_report_widget_qml_files_location/)). Beginning with version 6.6, the trash widget has been swapped to a compiled variant, making user modifications impossible without recompiling the Plasma project. As such, I'm keeping this version to allow me to use my modified version of this widget in newer Plasma releases.

## Differences from official widget

My main gripe with the official version of the widget is the icon which is used to convey the trash icon. 

By default, when creating a trash shortcut on the desktop as a `.desktop` entry, you can specify icons for both the full and empty trash states using **`Icon`** and **`EmptyIcon`** keys. When using the icon names **`user-trash-full`** and **`user-trash`**, the resulting look seems to fit the desktop:
* *Breeze Dark*
<img src="screenshots/breeze-dark desktop.png"  alt="Desktop trash icon with the Breeze Dark icon theme" width="200"> 

* *WhiteSur-dark*
<img src="screenshots/WhiteSur-dark desktop.png"  alt="Desktop trash icon with the WhiteSur-dark icon theme" width="200">

Whne using the org.kde.plasma.trash plasmoid/widget on the desktop, the visual behaviour is the same as in the case of the desktop entry.

When attempting to use the trash plasmoid on panels of larger than default heights (e.g. trying to construct a panel resembling the MacOS dock, along with an analogous trash can icon) the icons which is used seems inapropriate for large sizes:
* *Breeze Dark*
<img src="screenshots/breeze-dark before.png"  alt="Default plasmoid trash icon with the Breeze Dark icon theme" width="500">

* *WhiteSur-dark*
<img src="screenshots/WhiteSur-dark before.png"  alt="Default plasmoid trash icon with the WhiteSur-dark icon theme" width="500">

This is caused by the following code fragment:
```cpp
Plasmoid.icon: {
        let iconName = (hasContents ? "user-trash-full" : "user-trash");

        
        if (inPanel) {
            return iconName += "-symbolic";
        }

        return iconName;
    }
```
The icons which end up being used are **`user-trash-full-symbolic`** and **`user-trash-empty-symbolic`**, which in my humble opinion, just look bad. The fix was as simple as commenting/removing the IF statement. Now, the widget looks like this:
* *Breeze Dark*
<img src="screenshots/breeze-dark after.png"  alt="Modified plasmoid trash icon with the Breeze Dark icon theme" width="500">

* *WhiteSur-dark*
<img src="screenshots/WhiteSur-dark after.png"  alt="Modified plasmoid trash icon with the WhiteSur-dark icon theme" width="500">
