# Lovelace Cards Using Jinja2 Scripting

## This script auto generates Lovelace Entity Cards

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
...
...
```

