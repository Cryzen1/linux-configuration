### XFCE4 Configuration

- Desktop setup:

```bash
xfconf-query -c xfce4-desktop -p /desktop-icons/file-icons/show-filesystem -n -t string -s false
xfconf-query -c xfce4-desktop -p /desktop-icons/file-icons/show-home -n -t string -s false
xfconf-query -c xfce4-desktop -p /desktop-icons/file-icons/show-removable -n -t string -s false
xfconf-query -c xfce4-desktop -p /desktop-icons/file-icons/show-trash -n -t string -s false
```

- Panel setup:

```bash
xfconf-query -c xfce4-panel -p /panels/panel-2 -r -R
xfconf-query -c xfce4-panel -p /configver -n -t int -s 2
xfconf-query -c xfce4-panel -p /panels/dark-mode -n -t string -s true
xfconf-query -c xfce4-panel -p /panels/panel-1/icon-size -n -t int -s 22
xfconf-query -c xfce4-panel -p /panels/panel-1/length -n -t int -s 100
xfconf-query -c xfce4-panel -p /panels/panel-1/position-locked -n -t string -s true
xfconf-query -c xfce4-panel -p /panels/panel-1/size -n -t int -s 32
```

- Thunar setup:

```bash
xfconf-query -c thunar -p /default-view -n -t string -s ThunarDetailsView
xfconf-query -c thunar -p /last-details-view-column-widths -n -t string -s "50,126,124,50,50,50,50,50,530,226,111,263,50,152"
xfconf-query -c thunar -p /last-details-view-visible-columns -n -t string -s "THUNAR_COLUMN_DATE_ACCESSED,THUNAR_COLUMN_DATE_MODIFIED,THUNAR_COLUMN_NAME,THUNAR_COLUMN_SIZE,THUNAR_COLUMN_TYPE"
xfconf-query -c thunar -p /last-show-hidden -n -t string -s true
xfconf-query -c thunar -p /last-side-pane -n -t string -s ThunarShortcutsPane
xfconf-query -c thunar -p /last-toolbar-item-order -n -t string -s "0,1,2,3,4,5,6,7,8,9,12,13,14,15,11,10,16,17"
xfconf-query -c thunar -p /last-toolbar-visible-buttons -n -t string -s "0,1,1,1,0,0,0,0,0,0,0,0,1,0,1,1,1,1"
xfconf-query -c thunar -p /last-view -n -t string -s ThunarDetailsView
xfconf-query -c thunar -p /last-window-maximized -n -t string -s true
xfconf-query -c thunar -p /misc-date-custom-style -n -t string -s "%H:%M %d.%m.%Y"
xfconf-query -c thunar -p /misc-date-style -n -t string -s THUNAR_DATE_STYLE_CUSTOM
xfconf-query -c thunar -p /misc-directory-specific-settings -n -t string -s false
xfconf-query -c thunar -p /misc-full-path-in-tab-title -n -t string -s true
xfconf-query -c thunar -p /misc-single-click -n -t string -s false
```

- Appearance setup:

```bash
xfconf-query -c xsettings -p /Gtk/DecorationLayout -n -t string -s "close,maximize,minimize:menu"
xfconf-query -c xsettings -p /Net/IconThemeName -n -t string -s "Papirus-Dark"
xfconf-query -c xsettings -p /Net/ThemeName -n -t string -s "Fluent-round-grey-Dark"
xfconf-query -c xfwm4 -p /general/theme -n -t string -s "Fluent-round-grey-Dark"
xfconf-query -c xfwm4 -p /general/placement_ratio -n -t int -s 100
```

- Pointers setup:

```bash
xfconf-query -c pointers -p /Elan_Touchpad/Properties/libinput_Tapping_Enabled -n -t int -s 1
```
