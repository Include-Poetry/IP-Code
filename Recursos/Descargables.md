---
layout: G-Article
title: Recursos descargables
description: Porque por material no paramos, descarga todos los recursos necesarios para que empieces a programar
permalink: /Recursos/Descargables/
---

{% assign rawcats = "" %}
{% for elemento in site.Descargables %}
{% assign tcats = elemento.category | join:'|' | append:'|' %}
{% assign rawcats = rawcats | append:tcats %}
{% endfor %}

{% assign rawcats = rawcats | split:'|' | sort %}

{% assign cats = "" %}

{% for cat in rawcats %}
{% if cat != "" %}

{% if cats == "" %}
{% assign cats = cat | split:'|' %}
{% endif %}

{% unless cats contains cat %}
{% assign cats = cats | join:'|' | append:'|' | append:cat | split:'|' %}
{% endunless %}
{% endif %}
{% endfor %}

Todo el material recopilado aquí es de distribución libre, por lo que pueden ser encontrados también en el sitio de su autores.

Si estás buscando algún material relacionado, y no lo encuentras aquí, no dudes en mandar <a href="{{ site.url }}/Contacto/">un mensaje</a>. Sé muy específico con lo que buscas, y si lo tenemos disponible, te lo haremos llegar.

{% for ct in cats %}
{% if ct contains "lectura" %}
<h2>Material de lectura</h2>
{% endif %}
{% if ct contains "entrenamiento" %}
<h2>Plataformas de entrenamiento</h2>
{% endif %}
{% if ct contains "programas" %}
<h2>Programas</h2>
{% endif %}
<ul class="ListaTags">
    {% for elemento in site.Descargables %}
        {% if elemento.category contains ct %}
        <li>
            <h3>{{ elemento.title }}</h3>
            {{ elemento.content }}
            <p>
            	<a href="{{ elemento.download_original}}" target="_blank">Sitio oficial</a>
            	{% if elemento.download_iP %}
            	 | <a href="{{ elemento.download_iP}}" target="_blank">Desde #iP</a>
            	{% endif %}
            </p>
        </li>
        {% endif %}
    {% endfor %}
</ul>
{% endfor %}