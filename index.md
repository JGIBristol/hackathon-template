---
title: #MCMICRO hackathon 2022 
menu_title: Home
menu_icon: house-door
---


<div class="aside">
    <h2><i class="bi bi-calendar3"></i> Event timeline</h2>
    <dl>
        {% if site.registration_status == "soon" or site.registration_status == "open" or site.registration_status == "demo" %}
            <dt>{{ site.registration_opens_date }}</dt>
            <dd>
                Applications open for participants<br>
                {% if site.registration_status == 'open' %}
                    <a href="{{ site.baseurl }}{% link registration.md %}" class="btn">Register now</a>
                {% elsif site.registration_status == 'closed' %}
                    <a class="btn disabled">Registration has closed</a>
                {% elsif site.registration_status == 'soon' %}
                    <a class="btn disabled">Registration opens soon</a>
                {% endif %}
            </dd>
        {% endif %}

        <dt>{{ site.event_date }}</dt>
        <dd>Hackathon date</dd>
    </dl>
</div>

{% if site.event_status != "over" %}

<img src="./assets/advert.png" alt="Hackathon Logo" style="width:40%;height:20%;">
<br><br>
We are excited to announce our first ever MCMICRO hackathon in Heidelberg, brought to you by the Schapiro lab. The Hackathon will take place at the Marsilius Arkaden (Im Neuenheimer Feld 130.3, room K1, 69120 Heidelberg).

On this web page, you can find general information regarding the hackathon, like the [agenda](agenda.md), the [participants](about.md) as well as the [projects](projects.md) that we will be working on, as well as some [training resources](resources.md) about nextflow.

For more information on MCMICRO, please visit the [official MCMICRO main page](https://mcmicro.org/).

{% include youtube.html video="fnxBvgJQmtY" title="Image Analysis with MCMICRO - Overview" %}

# Sponsors
<br><br>
<img src="./assets/lunaphore_logo.png" alt="Lunaphore Logo" style="width:40%;height:20%;">

Coffee and food for this event are sponsored by Lunaphore technologies [https://lunaphore.com/](https://lunaphore.com/).

{% else %}

The first ever MCMICRO hackathon was a great success!

{% endif %}
