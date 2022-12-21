# CAUTION! ABANDONWARE AHEAD!

I have opted to archive this repo for several reasons:
1. I no longer have time to maintain this or fix any bugs.
2. Dark Sky is going away very soon (March 31st, 2023) due to it's purchase by Apple.
3. There are lots of other better alternatives now available on HACS that do the same thing, only better.

Thank you for your interest. This repo will remain public and available as a reference for others to use.

# Dark Sky Weather Card

[![hacs_badge](https://img.shields.io/badge/HACS-Default-orange.svg?style=for-the-badge)](https://github.com/custom-components/hacs) ![GitHub](https://img.shields.io/github/license/clayauld/lovelace-darksky-card?style=for-the-badge) ![GitHub last commit](https://img.shields.io/github/last-commit/clayauld/lovelace-darksky-card?style=for-the-badge) ![Maintenance](https://img.shields.io/maintenance/yes/2022?style=for-the-badge)

The Dark Sky Weather Card provides current and forecasted weather conditions using the Dark Sky platform. You configure the card by passing in sensor entities from the Dark Sky Sensor platform. 

Credit for the work goes to https://github.com/iammexx for his work in getting the card up and running. I merely made it compatible with HACS (https://hacs.xyz/). Add it to HACS by adding this repository in the Custom Repository menu and select "plugin" as the category.

The card is very customizable.  You can configure many aspects of its look and feel, as well as which specific content to show by passing in customization flags and defining optional sensors.  Content can also be rearranged if desired.

Hovering over a forecast day will display the daily weather summary in a tooltip popup if that option has been enabled.

Light Theme                |  Dark Theme
:-------------------------:|:-------------------------:
![image](https://raw.githubusercontent.com/clayauld/lovelace-darksky-card/master/images/light-theme.jpg)  |  ![image](https://raw.githubusercontent.com/clayauld/lovelace-darksky-card/master/images/dark-theme.jpg)

**Installation**
------------------------------
1. Search for Dark Sky Rich Weather Card in the HACS plugin list. Open it and click "Install" then "Add to Lovelace".

2. Download the amcharts icons from https://www.amcharts.com/dl/svg-weather-icons/ and put them in ```<config-dir>/www/icons/weather_icons```.  Create the directories if necessary.

You should end up with the following folders:

```<config-dir>/www/community/lovelace-darksky-card/lovelace-darksky-card.js```

```<config-dir>/www/icons/weather_icons/animated/```

```<config-dir>/www/icons/weather_icons/static/```

**Configuration**
------------------------------
1. Add the Dark Sky sensor platform to your configuration.yaml or sensors.yaml or wherever you keep your sensor configuration.

~~~~  
- platform: darksky
    api_key: <Your Dark Sky API Key>
    forecast:
      - 0
      - 1
      - 2
      - 3
      - 4
      - 5
    monitored_conditions:
      - icon
      - summary
      - nearest_storm_distance
      - nearest_storm_bearing
      - humidity
      - temperature
      - temperature_high
      - temperature_low
      - apparent_temperature
      - apparent_temperature_high
      - apparent_temperature_low
      - wind_speed
      - wind_bearing
      - precip_type
      - precip_probability
      - precip_accumulation
      - precip_intensity
      - precip_intensity_max
      - uv_index
      - daily_summary
      - pressure
      - visibility
    scan_interval:
      minutes: 5
~~~~

The next two steps are completed differently based on the version of HA you are using:
- Pre 0.84 or if using yaml mode in 0.84 or above : Add to your ui-lovelace.yaml file.
- Using storage mode in 0.84 or above use the "Raw Config Editor" to add the reference and definition to the config.

2. Check to see if HACS has added the resource to your Home Assistant config. Go to Configration -> Lovelace Dashboards -> Resources.

**Note: Ensure type is set to module and not js**
**Note: /local/ points to the <config-dir>/www/ directory.**

~~~~
resources:
  - url: /local/community/lovelace-darksky-card/lovelace-darksky-card.js
    type: module
~~~~

**Note: If the resource is not properly found you may need to edit the url to the following:**

~~~~
resources:
  - url: /local/community/lovelace-darksky-card/lovelace-darksky-card.js?v=7.1
    type: module
~~~~

3. Add the card definition:  There are required / optional and flag entries.  

Required entries must be present 
in your configuration.  The card will not work at all if any of these lines are missing. 
~~~~
type: 'custom:lovelace-darksky-card'
entity_current_conditions: sensor.dark_sky_icon
entity_temperature: sensor.dark_sky_temperature
entity_summary_today: sensor.dark_sky_summary_0d
entity_daily_summary: sensor.dark_sky_daily_summary
entity_forecast_high_temp_1: sensor.dark_sky_daytime_high_temperature_1d
entity_forecast_high_temp_2: sensor.dark_sky_daytime_high_temperature_2d
entity_forecast_high_temp_3: sensor.dark_sky_daytime_high_temperature_3d
entity_forecast_high_temp_4: sensor.dark_sky_daytime_high_temperature_4d
entity_forecast_high_temp_5: sensor.dark_sky_daytime_high_temperature_5d
entity_forecast_icon_1: sensor.dark_sky_icon_1d
entity_forecast_icon_2: sensor.dark_sky_icon_2d
entity_forecast_icon_3: sensor.dark_sky_icon_3d
entity_forecast_icon_4: sensor.dark_sky_icon_4d
entity_forecast_icon_5: sensor.dark_sky_icon_5d
entity_forecast_low_temp_1: sensor.dark_sky_overnight_low_temperature_0d
entity_forecast_low_temp_2: sensor.dark_sky_overnight_low_temperature_1d
entity_forecast_low_temp_3: sensor.dark_sky_overnight_low_temperature_2d
entity_forecast_low_temp_4: sensor.dark_sky_overnight_low_temperature_3d
entity_forecast_low_temp_5: sensor.dark_sky_overnight_low_temperature_4d
entity_summary_1: sensor.dark_sky_summary_1d
entity_summary_2: sensor.dark_sky_summary_2d
entity_summary_3: sensor.dark_sky_summary_3d
entity_summary_4: sensor.dark_sky_summary_4d
entity_summary_5: sensor.dark_sky_summary_5d
~~~~

Optional entries add components to the card. 
***Please note entity_pop_1 to 5 lines must all be included for daily pop (probability of precip) to show in forecast
~~~~
entity_sun: sun.sun
entity_visibility: sensor.dark_sky_visibility
entity_daytime_high: sensor.dark_sky_daytime_high_temperature_0d
entity_wind_bearing: sensor.dark_sky_wind_bearing
entity_wind_speed: sensor.dark_sky_wind_speed
entity_humidity: sensor.dark_sky_humidity
entity_pressure: sensor.dark_sky_pressure
entity_apparent_temp: sensor.dark_sky_apparent_temperature
entity_pop: sensor.dark_sky_precip_probability
entity_pop_intensity: sensor.dark_sky_precip_intensity
entity_pop_1: sensor.dark_sky_precip_probability_1d
entity_pop_2: sensor.dark_sky_precip_probability_2d
entity_pop_3: sensor.dark_sky_precip_probability_3d
entity_pop_4: sensor.dark_sky_precip_probability_4d
entity_pop_5: sensor.dark_sky_precip_probability_5d
~~~~

**Note:** The following entries require template sensors.  The alt_* entries are for overriding the text for the indicated slot entry. By using these you can create whatever format you like for these entries.
~~~~
entity_current_text: sensor.dark_sky_current_text
alt_daytime_high: sensor.dark_sky_alt_daytime_high 
alt_wind: sensor.dark_sky_alt_wind
alt_visibility: sensor.dark_sky_alt_visibility
alt_pop: sensor.dark_sky_alt_pop
alt_pressure: sensor.dark_sky_alt_pressure
alt_humidity: sensor.dark_sky_alt_humidity
~~~~

**Example template sensors:** You can call template sensors whatever you want so long as you use the same name in the card config.  
~~~~~
      dark_sky_current_text:
        value_template:  
           '{% if is_state("sensor.dark_sky_icon","clear-day") %} Clear 
            {% elif is_state("sensor.dark_sky_icon","clear-night") %} Clear 
            {% elif is_state("sensor.dark_sky_icon","rain") %} Rain
            {% elif is_state("sensor.dark_sky_icon","snow") %} Snowy
            {% elif is_state("sensor.dark_sky_icon","fog") %} Foggy
            {% elif is_state("sensor.dark_sky_icon","sleet") %} Sleet
            {% elif is_state("sensor.dark_sky_icon","wind") %} Windy
            {% elif is_state("sensor.dark_sky_icon","cloudy") %} Cloudy
            {% elif is_state("sensor.dark_sky_icon","partly-cloudy-day") %} Partly Cloudy
            {% elif is_state("sensor.dark_sky_icon","partly-cloudy-night") %} Partly Cloudy
            {% elif is_state("sensor.dark_sky_icon","hail") %} Hailing
            {% elif is_state("sensor.dark_sky_icon","lightning") %} Lightning
            {% elif is_state("sensor.dark_sky_icon","thunderstorm") %} Thunderstorm
            {% endif %}'
                         
      dark_sky_alt_wind:
        value_template: >-
                        {% set winddir = ['North','North-Northeast','Northeast','East-Northeast','East','East-Southeast','Southeast','South-Southeast','South','South-Southwest','Southwest','West-Southwest','West','West-Northwest','Northwest','North-Northwest','North'] %}
                        {{ states('sensor.dark_sky_wind_speed') | round }} mi/h from the {{ winddir[((states('sensor.dark_sky_wind_bearing') | float / 360)*16) | round]}}
~~~~~

Flags are used to control the look and feel of the card (See below for details)
~~~~
locale: en
static_icons: false
tooltip_bg_color: 'rgb( 75,155,239)'
tooltip_border_color: orange
tooltip_border_width: 3
tooltip_caret_size: 10
tooltip_fg_color: '#fff'
tooltip_left_offset: -12
tooltip_width: 100
tooltips: true
old_daily_format: false
time_format: 24
show_beaufort: true
~~~~

**Flags**
--------------------------
| Flag                     | Values                      | Usage                                                                       |
|--------------------------|-----------------------------|-----------------------------------------------------------------------------|
| locale                   | **en** / fr / de / etc.     | Sets locale display of day names and time formats                           |
| static_icons             | true / **false**            | Switches between static (true) and animated (false) icons                   |
| tooltips                 | true / **false**            | Enables tooltips that show daily forecast summary                           |
| tooltip_width            | **110**                     | Sets the width of the tooltip in px                                         |
| tooltip_bg_color         | **rgb( 75,155,239)**        | Sets the background color of the tooltip (rgb / # / color)                  |
| tooltip_fg_color         | **#fff**                    | Sets the foreground color of the tooltip (rgb / # / color)                  |
| tooltip_border_color     | **rgb(255,161,0)**          | Sets the color of the tooltip border including the caret (rgb / # / color)  |
| tooltip_border_width     | **1**                       | Sets the width of the tooltip border in px                                  |
| tooltip_caret_size       | **5**                       | Sets the size of the caret (the little arrow pointing down) in px           |
| tooltip_left_offset      | **-12**                     | Sets the offset of the left edge of the tooltip. In negative (-)x           |
| refresh_interval         | **30** / Integer value      | Sets the nuber of seconds between card value refreshes                      |
| old_daily_format         | true / **false**            | Sets the format of the daily high & low temps to be stacked (old format)    |
| show_beaufort            | true / **false**            | Shows Beaufort Scale wind information                                       |
| show_separator           | true / **false**            | Shows separator between current conditions columns and current temp / Icon  |
| time_format              | **locale** / 12 / 24        | Sets the format sunset and sunrise times. locale format is the default.     |
| temp_top_margin          | **-.3em** / px or em value  | Sets the top margin of the Temperature.                                     |
| temp_font_weight         | **300** / numeric value     | Sets the font weight of the Temperature.                                    |
| temp_font_size           | **4em** / em value          | Sets the font size of the Temperature.                                      |
| temp_right_pos           | **.85em** / px or em value  | Sets the right position of the Temperature.                                 |
| temp_uom_top_margin      | **-9px** / px or em value   | Sets the top margin of the Temperature Unit of Meaure.                      |
| temp_uom_right_margin    | **7px** / px or em value    | Sets the right margin of the Temperature Unit of Measure.                   |
| apparent_top_margin      | **39px** / px or em value   | Sets the top margin of the apparent (feels Like) temperature                |
| apparent_right_pos       | **1em** / px or em value    | Sets the right position of the apparent (feels Like) temperature            |
| apparent_right_margin    | **1em** / px or em value    | Sets the right margin of the apparent (feels Like) temperature              |
| current_text_top_margin  | **39px** / px or em value   | Sets the top margin of the current temperature text                         |
| current_text_left_pos    | **5em** / px or em value    | Sets the left position of the current temperature text                      |
| current_text_font_size   | **1.5em** / em value        | Sets the font size of the current temperature text                          |
| current_data_top_margin  | **6em** / px or em value    | Sets the top margin of the current data blocks                              |
| large_icon_top_margin    | **-3.5em** / px or em value | Sets the top margin of the current conditions icon                          |
| large_icon_left_position | **0em** / px or em value    | Sets the left position of the current conditions icon                       |
| separator_top_margin     | **5em** / px or em value    | Sets the top margin of the separator line                                   |
| slot_l1                  | **daytime_high**            | Sets the value used in current conditions slot l1 : See slots for more info |
| slot_l2                  | **wind**                    | Sets the value used in current conditions slot l2 : See slots for more info |
| slot_l3                  | **visibility**              | Sets the value used in current conditions slot l3 : See slots for more info |
| slot_l4                  | **sun_next**                | Sets the value used in current conditions slot l4 : See slots for more info |
| slot_r1                  | **pop**                     | Sets the value used in current conditions slot r1 : See slots for more info |
| slot_r2                  | **humidity**                | Sets the value used in current conditions slot r2 : See slots for more info |
| slot_r3                  | **pressure**                | Sets the value used in current conditions slot r3 : See slots for more info |
| slot_r4                  | **sun_following**           | Sets the value used in current conditions slot r4 : See slots for more info |


**Slots**
--------------------------
The current condition columns are specified by 'slots'.  There are 4 left column slots (designated l1 - l4) and 4 right column
slots (designated r1 - r4).  There are currently 10 possible values that can be assigned to a slot.  These are:
- daytime_high
- wind
- visibility
- sun_next (the next sun event ... sunset or sunrise)
- sun_following (The following sun event ... if sun_next is a sunset then this will be the following sunrise and vice versa)
- pop (probability of precipitation)
- humidity
- pressure
- empty (empty slot... the slot below does not rise to fill the space)
- remove (same as empty but the slot below rises to take the place of the slot)
