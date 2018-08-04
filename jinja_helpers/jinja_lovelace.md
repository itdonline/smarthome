# Lovelace Cards Using Jinja2 Scripting

## 1. This script auto generates Lovelace Entity Cards

```
{% set domains = states | map(attribute='domain') |list | unique | list %}
{%- for item in domains -%}
- type: entities
  title: {{ item.replace('_', ' ') | title }}
  show_header_toggle: true
  entities:
{%- for e in states[item] %}
    - {{ e.entity_id }}
      name: {{ e.name }}
{%- endfor %}

{% endfor -%}
```

The output of the above script would look like the following:

```
# This script auto generates Lovelace Entity Cards

- type: entities
  title: Alarm Control Panel
  show_header_toggle: true
  entities:
    - alarm_control_panel.simplisafe
      name: Home Security System

- type: entities
  title: Sun
  show_header_toggle: true
  entities:
    - sun.sun
      name: Sun
      
- type: entities
  title: Proximity
  show_header_toggle: true
  entities:
    - proximity.home
      name: home
    - proximity.work
      name: work

...
```

## 2. This script auto generates Lovelace Entity-Filter Card for your Device Trackers

```
{% for item in states['device_tracker'] -%}
- type: entity-filter
  state_filter:
    - 'home'
  card:
    type: glance
    title: My Device Trackers
  entities:
{%- for e in states[item] %}
    - {{ e.entity_id }}
{%- endfor %}
{% endfor %}
```
The output of above would look something like:

```
- type: entity-filter
  state_filter:
    - 'home'
  card:
    type: glance
    title: My Device Trackers
  entities:
    - device_tracker.hasika_hasika
    - device_tracker.ipad
    - device_tracker.mallika_mallika
    - device_tracker.srinika_srinika
    - device_tracker.suresh_suresh
    - device_tracker.tesla_model_3_5yj3e1ea8jf010610_location_tracker
```
