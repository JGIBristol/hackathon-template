---
layout: page
title: Template Hackathon
menu_title: Home
menu_icon: house-door
---

{:.secondary}
# {{ site.event_date }}, in association with the University of Bristol

<!-- REMOVE THIS SECTION when you use this template -->
<div class="lead" markdown="1">
This is a demo of the template repository for a public-facing hackathon website,
built by the [Jean Golding Institute](https://www.bristol.ac.uk/golding/) at the
University of Bristol.

For more information: view the [README](https://github.com/jgibristol/hackathon-template/blob/main/README.md) 
or the [GitHub repository](https://github.com/jgibristol/hackathon-template).
</div>
<!-- END of section to remove -->

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

        <dt>{{ site.registration_closes_date }}</dt>
        <dd>Applications close</dd>

        <dt>{{ site.event_date }}</dt>
        <dd>Hackathon date</dd>
    </dl>
</div>

{% if site.event_status != "over" %}

Scientists from the University of Bristol are hosting a X-day hackathon on
{{ site.event_date }}, open to researchers, to...

Researchers can sign up to [topics ranging from]({{ site.baseurl }}{% link projects.md %})
... to ..., and more. Teams will be led by senior academics from a range of
disciplines at the University of Bristol, but participating researchers can be
from any UK academic institution. [This opportunity]({{ site.baseurl }}{% link registration.md %})
is open to early career researchers[<sup>(?)</sup>][faq]{:title="What do we mean by an Early Career Researcher (ECR)?"}.

Participation is open to **researchers from any UK academic institution**, and
we encourage contributions from **early career researchers**[<sup>(?)</sup>][faq]{:title="What do we mean by an Early Career Researcher (ECR)?"},
including PhDs and Postdocs.

## Logistics

The event will take place virtually, using a combination of **video
conferencing** (Zoom) for meetings and seminars, and **discussion forums**
(Slack) for ongoing comms. Data holding and analysis will take place on...

## Outputs

By the end of the event, we hope to...

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
