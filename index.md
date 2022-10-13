---
layout: page
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

We are excited to announce our first ever MCMicro hackathon in Heidelberg, brought to you by the Schapiro lab.

[faq]: {{ site.baseurl }}{% link faq.md %}

{% else %}

Scientists from the University of Bristol hosted a X-day hackathon on
{{ site.event_date }}, open to researchers, to...

Researchers could sign up to [topics ranging from]({{ site.baseurl }}{% link projects.md %})
... to ..., and more. Teams were be led by senior academics from a range of
disciplines at the University of Bristol, but participating researchers could be
from any UK academic institution.

The event took place virtually, using a combination of **video conferencing**
(Zoom) for meetings and seminars, and **discussion forums** (Slack) for ongoing
comms. Data holding and analysis took place on...

{% endif %}
