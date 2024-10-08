# Panel Configuration
The `Configuration` tab of settings dialog allows you to configure the behavior of the HyprPanel. You can access the Configuration tab by clicking the category `Configuration` in the settings dialog.

![Configuration Tab](../images/configuration/configuration/configuration_tab.png)

The Configuration tab contains the following categories that you can configure.

## General
The **General** tab contains your font settings and your default terminal. The font size you select will determine the scaling of your entire panel.

The **Default Terminal** determines which terminal emulator to use when opening a terminal command from the panel.

Additionally, this is where you can **Import** or **Export** your HyprPanel configuration.

## Bar
This is where you can configure the behavior of the panel bar. The options in this tab let you configure the panel's behavior and the settings of all the modules that are displayed on the bar.

### Layouts
The **Layouts** section allows you to configure the layout of the panel. If you want to display specific modules in a specific order, you can do so by defining a layout object that configures the layout of your bar for each monitor. By default, the layout is as follows:
```json
{
    "0": {
        "left": [
            "dashboard",
            "workspaces",
            "windowtitle"
        ],
        "middle": [
            "media"
        ],
        "right": [
            "volume",
            "network",
            "bluetooth",
            "systray",
            "clock",
            "notifications"
        ]
    },
    "1": {
        "left": [
            "dashboard",
            "workspaces",
            "windowtitle"
        ],
        "middle": [
            "media"
        ],
        "right": [
            "volume",
            "clock",
            "notifications"
        ]
    },
    "2": {
        "left": [
            "dashboard",
            "workspaces",
            "windowtitle"
        ],
        "middle": [
            "media"
        ],
        "right": [
            "volume",
            "clock",
            "notifications"
        ]
    },
}
```
The numbers `0`, `1`, and `2` represent the monitor index. The `left`, `middle`, and `right` keys represent the modules that will be displayed on the left, middle, and right side of the panel, respectively. Each section (left, middle, right) is an array of module names that will be displayed in the order they are listed. You can select from the following modules:
```js
"battery"
"dashboard"
"workspaces"
"windowtitle"
"media"
"notifications"
"volume"
"network"
"bluetooth"
"clock"
"systray"
```

#### Hiding the Bar on specific monitors
You may decide that you only want to display the bar on your primary monitor; you can hide the bar on any monitor by assigning an empty array to each section.

In the following example, if your primary monitor is `"0"`, you can hide the bar on monitors `"1"` and `"2"` by setting the layout as follows:
```json
{
    "0": {
        "left": [
            "dashboard",
            "workspaces",
            "windowtitle"
        ],
        "middle": [
            "media"
        ],
        "right": [
            "volume",
            "network",
            "bluetooth",
            "systray",
            "clock",
            "notifications"
        ]
    },
    "1": {
        "left": [],
        "middle": [],
        "right": []
    },
    "2": {
        "left": [],
        "middle": [],
        "right": []
    }
}
```
### Spacing
This section allows you to configure the spacing of the bar and the modules inside of it. This is also where you can configure your bar to be floating or docked. If your bar is floating, you can configure the position of the bar on the screen and the radius of the corners.

### Dashboard
This section allows you to change the icon of your dashboard module in the bar if you're not using **Arch by the way**.

### Workspaces
This section allows you to configure the behavior of the workspace module. You can configure the number of workspaces, how workspaces are represented, whether the workspace module should display the workspaces specific to the monitors, the scroll behavior, and the workspace icon spacing.

### Window Titles
Window titles display the name of the currently focused window. This section lets you configure the spacing between the icon and the label/name of the currently focused window.

#### Window Title Mappings
Window title mappings allow you to assign a specific icon and a name to specified window in the window titles bar module. This mapping is an array of arrays where each array contains the following:
- The **original window title** in all lowercase (can be a regular expression)
- The **icon** to display
- The **replacement window title** to display

Example of window mappings - notice that the nerd font icon may not render correctly in the browser:
```json
[
    ["kitty", "󰄛", "Kitty Terminal"],
    ["firefox", "󰈹", "Firefox"],
    ["microsoft-edge.*", "󰇩", "Edge"],
    ["discord", "", "Discord"],
    ["org.kde.dolphin", "", "Dolphin"],
]
```
Note that you must provide the original window title in all ***lowercase***. If you have nothing mapped to a specific window title, the default window title will be displayed in the module.
### Volume
This section allows you to configure the volume module. You can configure the inner spacing and toggle the volume label.

### Network
The network module displays your network status. This section allows you to configure the inner spacing, toggle the network label and determine the truncation of the network name.

### Bluetooth
The bluetooth module displays your bluetooth status. This section allows you to configure the inner spacing and toggle the bluetooth label.

### Clock
You can define the format of the clock displayed in the clock module in this section. This format is the strftime() format language as specified by c99.

Here are all the time format specifiers:
```bash
%a: the abbreviated weekday name according to the current locale
%A: the full weekday name according to the current locale
%b: the abbreviated month name according to the current locale
%B: the full month name according to the current locale
%c: the preferred date and time representation for the current locale
%C: the century number (year/100) as a 2-digit integer (00-99)
%d: the day of the month as a decimal number (range 01 to 31)
%e: the day of the month as a decimal number (range 1 to 31); single digits are preceded by a figure space (U+2007)
%F: equivalent to `Y-%m-%d` (the ISO 8601 date format)
%g: the last two digits of the ISO 8601 week-based year as a decimal number (00-99). This works well with V and %u.
%G: the ISO 8601 week-based year as a decimal number. This works well with V and %u.
%h: equivalent to %b
%H: the hour as a decimal number using a 24-hour clock (range 00 to 23)
%I: the hour as a decimal number using a 12-hour clock (range 01 to 12)
%j: the day of the year as a decimal number (range 001 to 366)
%k: the hour (24-hour clock) as a decimal number (range 0 to 23); single digits are preceded by a figure space (U+2007)
%l: the hour (12-hour clock) as a decimal number (range 1 to 12); single digits are preceded by a figure space (U+2007)
%m: the month as a decimal number (range 01 to 12)
%M: the minute as a decimal number (range 00 to 59)
%f: the microsecond as a decimal number (range 000000 to 999999)
%p: either ‘AM’ or ‘PM’ according to the given time value, or the corresponding strings for the current locale. Noon is treated as ‘PM’ and midnight as ‘AM’. Use of this format specifier is discouraged, as many locales have no concept of AM/PM formatting. Use %c or X instead.
%P: like %p but lowercase: ‘am’ or ‘pm’ or a corresponding string for the current locale. Use of this format specifier is discouraged, as many locales have no concept of AM/PM formatting. Use %c or X instead.
%r: the time in a.m. or p.m. notation. Use of this format specifier is discouraged, as many locales have no concept of AM/PM formatting. Use %c or X instead.
%R: the time in 24-hour notation (H`:`M)
%s: the number of seconds since the Epoch, that is, since 1970-01-01 00:00:00 UTC
%S: the second as a decimal number (range 00 to 60)
%t: a tab character
%T: the time in 24-hour notation with seconds (H`:`M`:`S)
%u: the ISO 8601 standard day of the week as a decimal, range 1 to 7, Monday being 1. This works well with G and V.
%V: the ISO 8601 standard week number of the current year as a decimal number, range 01 to 53, where week 1 is the first week that has at least 4 days in the new year. See g_date_time_get_week_of_year(). This works well with G and %u.
%w: the day of the week as a decimal, range 0 to 6, Sunday being 0. This is not the ISO 8601 standard format — use %u instead.
%x: the preferred date representation for the current locale without the time
%X: the preferred time representation for the current locale without the date
%y: the year as a decimal number without the century
%Y: the year as a decimal number including the century
%z: the time zone as an offset from UTC (+hhmm)
%:z: the time zone as an offset from UTC (+hh:mm). This is a gnulib strftime() extension. Since: 2.38
%::z: the time zone as an offset from UTC (+hh:mm:ss). This is a gnulib strftime() extension. Since: 2.38
%:::z: the time zone as an offset from UTC, with : to necessary precision (e.g., -04, +05:30). This is a gnulib strftime() extension. Since: 2.38
%Z: the time zone or name or abbreviation
%%: a literal % character
```

### Media
This section allows you to configure the media module. You can configure the inner spacing, the media label, and the truncation of the media name.

### Notifications
This section allows you to configure the notifications module. You can configure the inner spacing and whether or not to show the total number of notifications.
## Notifications
The **Notification Menu** tab allows you to configure the behavior of the notifications that are displayed by the HyprPanel. You can access the Notification Menu tab by clicking the category `Notifications` in the settings dialog.

In the **Notification Menu** tab, you can configure:
- The position of the notifications toast
- The timeout of the notifications toast
- Which monitor to display the notifications on
- Whether to follow the focused monitor
- Whether or not to preserve actions inside the notifications between sessions
  - Actions include buttons that are displayed in the notification that you can click on to perform an action

## OSD (On-Screen Display)
The **OSD** tab allows you to configure the behavior of the on-screen display that is displayed by the HyprPanel. You can access the OSD tab by clicking the category `OSD` in the settings dialog.

The OSD is displayed when you change the volume, brightness, or when you mute your audio. In the **OSD** tab, you can configure:
- Whether to show the OSD
- The orientation of the OSD
- The position of the OSD on the screen
- The monitor on which to display the OSD
- Whether to follow the focused monitor
- The Radius of the OSD corners
- The margin of the OSD from the edge of the screen

## Clock Menu
The **Clock Menu** tab allows you to configure the behavior of the clock module that is displayed by the HyprPanel. You can access the Clock Menu tab by clicking the category `Clock Menu` in the settings dialog.

The Clock Menu displays the time, calendar, and the weather. In the **Clock Menu** tab, you can configure:
- Whether to use 24-hour time
- Settings for the weather module
  - The weather location
  - The weather unit
  - The weather API key
  - The weather refresh rate

The Weather API key is required to fetch weather data. You can get a free API key from [WeatherAPI's Website](https://weatherapi.com/)
## Dashboard Menu
The **Dashboard Menu** tab allows you to configure the behavior of the dashboard module that is displayed by the HyprPanel. You can access the Dashboard Menu tab by clicking the category `Dashboard Menu` in the settings dialog.

The Dashboard Menu displays the dashboard, which is a menu that allows you to configure the following.

### Power Menu
The power menu section contains the system power options and the profile card which contains the user profile name and profile picture. 

You can configure the following in the Power Menu section:
- The user profile image
- The user profile name
- Enable/Disable confirmation dialog for power operations
- A custom command for the following power options:
  - Shutdown
  - Reboot
  - Sleep
  - Logout

### Resource Usage Metrics
If you have an NVidia GPU, you can enable the GPU usage bar in the dashboard.

### Shortcuts
This section allows you to configure the shortcuts that are displayed in the dashboard. There are a total of 8 shortcuts our of which 6 are user-configurable. 

You can configure the following for each of these 6 shortcuts:
- The icon
- The tooltip
- The command

The 2 non-configurable shortcuts are:
- The screen recording shortcut
- The settings shortcut

### Directories
The directories section allows you to configure the directories that are displayed in the dashboard. Although by default, the directories are configured to open the dolphin file manager, you can configure them to open any file manager of your choice at any specified drive. Additionally, you can configure this section to run any command if you desire to not have any directory shortcuts.

Each entry in the directories section contains the following configurable options:
- The Label/Name of the directory
- The command to run when the label is clicked
