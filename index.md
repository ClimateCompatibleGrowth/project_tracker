---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: home
---

{% leaflet_map {"zoom" : 2,
                "center" : [50, -114],
                "providerBasemap": "OpenStreetMap.HOT"} %}

{% for row in site.data.projects %}
    {% capture url %}<a href={{ row["website"] }} target='_blank'> {{ row["name"] }} </a><p>{{ row['short_description'] }}</p>{%endcapture%}
    {% capture coordinates %}{{row["lon"]}}, {{row["lat"]}}{% endcapture %}
    {% leaflet_geojson
    {   "type": "Feature",
        "properties": {"popupContent": "{{url}}"},
        "geometry": {
            "type": "Point",
            "coordinates": [ {{coordinates}} ],
            }} %}
{% endfor %}

{% endleaflet_map %}