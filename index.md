 
title: MCMicro hackathon 2022 
menu_title: Home
menu_icon: house-door
---

{:.secondary}
# {{ site.event_date }}


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

We are excited to announce our first ever MCMicro hackathon in Heidelberg, brought to you by the Schapiro lab.

[faq]: {{ site.baseurl }}{% link faq.md %}

{% else %}

The first ever MCMICRO hackathon was a great success!

{% endif %}
