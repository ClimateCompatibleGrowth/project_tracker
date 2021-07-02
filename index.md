---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: home
---

{% leaflet_map {"zoom" : 2,
                "center" : [50, 0],
                "providerBasemap": "OpenStreetMap"} %}

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

<ul>{% for row in site.data.projects %}<h1>
<a href="{{ row['website'] }}">{{ row['name'] }}</a></h1>
<p><b>Country:</b> {{ row['country'] }}</p>
<p><b>Main Contact:</b> {{ row['main_contact'] }}</p>
<p><b>Lead Institution:</b> {{ row['lead_institution'] }}</p>
<p><b>Start Date:</b> {{ row['start_date'] }}</p>
<p><b>End Date:</b> {{ row['end_date'] }}</p>
<p><b>Description:</b> {{ row['short_description'] }}</p>
  {% endfor %}
</ul>

{%- comment -%} <table>
{% tablerow row in site.data.projects %}
  <a href="{{ row['website'] }}">{{ row['name'] }}</a>
{% endtablerow %}
</table> {%- endcomment -%}
