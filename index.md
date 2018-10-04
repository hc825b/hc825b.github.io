---
layout: default
title: Chiao 橋
---

## About Chiao

I am a PhD student in [CS @ Illinois] and research in
[Programming Languages, Formal Methods, and Software Engineering][PL/FM/SE]
area.
Currently, I am doing research with my advisor, [Prof. Sayan Mitra][mitras],
and work as a graduate research assistant at [Information Trust Institute][ITI].

[CS @ Illinois]: https://cs.illinois.edu/
[PL/FM/SE]: https://cs.illinois.edu/research/programming-languages-formal-methods-and-software-engineering
[mitras]: http://mitras.ece.illinois.edu/
[ITI]: https://iti.illinois.edu/

## Posts

<ul class="posts">
  {% for post in site.posts %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>

