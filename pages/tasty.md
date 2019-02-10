---
title: Reading room
permalink: /docs/

layout: page
sidenav: docs

subnav:
  - text: Section one
    href: '#section-one'
  - text: Section two
    href: '#section-two'
---

{% block head_css_page %}
    <style type="text/css">
        #FOIASuprise {
            position: relative;
        }

        {% for position in positions %}
            #{{ position.redaction.redaction_id }}{{ position.id }} {
                position: absolute;
                top: {{ position.px_top }}px;
                left: {{ position.px_left }}px;
                color: {{ document.text_color }};
                /*font: 15px/35px , Courier, Serif;*/
                background: rgb(0, 0, 0); /* fallback color */
                background: {{ document.background_color }};
                font-size: 25px;
                font: Courier, Serif;*/
                padding:5px;
                padding-right:10px;
                padding-left:10px;
            }
        {% endfor %}
    </style>
{% endblock head_css_page %}

{% block content %}
<section class="usa-grid">
<h1>{{ document.name }} mad libs</h1>

<div id="main">
<div id="FOIASuprise">
    <img src="{{ document.image.url }}" alt="{{ document.discription }}">
    {% for position in positions %}
        <span id="{{ position.redaction.redaction_id }}{{ position.id }}" class='redaction'></span>
        <!-- EXAMPLE: <h2 id="food1" class="redaction"></h2> -->
    {% endfor %}
    <p>FOIA via <a href="{{ }}{{ document.source_url }}">{{ document.source }}</a></p>
</div>

<form name="FOIAForm" onsubmit="validateForm()" >
    {% for r in redactions %}
        {{ r.clue }}: <input id="{{ r.redaction_id }}">
    {% endfor %}

<button type="button" onclick="validateForm()">Submit</button>
</form>
</div>
</section>
{% endblock %}

{% block bottom_js %}
    <script>
        var x = document.getElementById("FOIASuprise");
        x.style.display = "none"

        function validateForm() {
            {% for position in positions %}
                var {{ position.redaction.redaction_id }} = document.forms["FOIAForm"]["{{ position.redaction.redaction_id }}"].value;
                document.getElementById("{{ position.redaction.redaction_id }}{{ position.id }}").innerHTML = {{ position.redaction.redaction_id }};

            // for some reason this end tag will break the form, I don't see a difference in the HTML so this is weird
            // {% endfor %}

            x.style.display = "block"
        }
    </script>
{% endblock %}

