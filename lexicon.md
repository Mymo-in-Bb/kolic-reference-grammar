---
title: Lexicon
description: Kolic Reference Grammar
---

This lexicon documents words that have been featured in WotW so far, and some other that haven't been featured yet.

# The Kolic - English Dictionary

[A](#ke-a) · [Á](#ke-á) · [Ä](#ke-ä) · [B](#ke-b) · [D](#ke-d) · [Ð](#ke-ð) · [E](#ke-e) · [É](#ke-é) · [Ë](#ke-ë) · [F](#ke-f) · [G](#ke-g) · [H](#ke-h) · [I](#ke-i) · [Í](#ke-í) · [J](#ke-j) · [K](#ke-k) · [L](#ke-l) · [M](#ke-m) · [N](#ke-n) · [O](#ke-o) · [Ó](#ke-ó) · [Ö](#ke-ö) · [P](#ke-p) · [R](#ke-r) · [S](#ke-s) · [T](#ke-t) · [Þ](#ke-þ) · [U](#ke-u) · [Ú](#ke-ú) · [V](#ke-v) · [Y](#ke-y) · [Ý](#ke-ý)

{% assign words = site.data.words.words | sort: "kolic" %}
{% assign alphabet = site.data.alphabet.kolic %}


{% assign grouped_words = words | group_by_exp: "item", "item.kolic | downcase | slice: 0, 1" %}

{% for letter in alphabet %}
{% for group in grouped_words %}
{% if group.name == letter %}
<h2 id="ke-{{ group.name }}">{{ group.name | upcase }}</h2>
{% assign kolic_terms = group.items | group_by_exp: "item", "item.kolic | append: '-' | append: item.broad | append: '-' | append: item.narrow" %}
{% for kolic_term in kolic_terms %}
{% capture entry %}
{% assign first_word = kolic_term.items[0] %}
**{{ first_word.kolic }}** /{{ first_word.broad }}/ [{{ first_word.narrow }}]<br>
{% for def in kolic_term.items %}
{% assign other = "" %}
{% if def.other %}
{% assign other = ", " | append: def.other %}
{% endif %}
{% assign tumblr = "" %}
{% if def.tumblr %}
{% assign tumblr = " ([WotW entry](" | append: def.tumblr | append: "))" %}
{% endif %}
{% if def.pos == "noun" %}
{% capture secondline %}*(noun, {{ def.gender }}{{ other }})* - **{{ def.english }}**{{ tumblr }}{% endcapture %}
{% elsif def.pos == "verb" %}
{% capture secondline %}*(verb, {{ def.transitivity }}{{ other }})* - **{{ def.english }}**{{ tumblr }}{% endcapture %}
{% elsif def.pos == "adverb" %}
{% capture secondline %}*(adverb{{ other }})* - **{{ def.english }}**{{ tumblr }}{% endcapture %}
{% elsif def.pos == "adjective" %}
{% capture secondline %}*(adjective{{ other }})* - **{{ def.english }}**{{ tumblr }}{% endcapture %}
{% else %}
{% capture secondline %}*({{ def.pos }}{{ other }})* - **{{ def.english }}**{{ tumblr }}{% endcapture %}
{% endif %}
&emsp;{{ forloop.index }}. {{ secondline }}<br>
{% if def.note %}
&emsp;&emsp;{{def.note}}<br>
{% endif %}
{% endfor %}
{% endcapture %}
{{ entry | strip_newlines }}
{% endfor %}
{% endif %}
{% endfor %}
{% endfor %}

---
<br>
# The English - Kolic Dictionary

[A](#ek-a) · [B](#ek-b) · [C](#ek-c) · [D](#ek-d) · [E](#ek-e) · [F](#ek-f) · [G](#ek-g) · [H](#ek-h) · [I](#ek-i) · [J](#ek-j) · [K](#ek-k) · [L](#ek-l) · [M](#ek-M) · [N](#ek-n) · [O](#ek-o) · [P](#ek-p) · [Q](#ek-q) · [R](#ek-r) · [S](#ek-s) · [T](#ek-t) · [U](#ek-u) · [V](#ek-v) · [W](#ek-w) · [X](#ek-x) · [Y](#ek-y) · [Z](#ek-z) 

{% assign words = site.data.words.words | sort: "english" %}
{% assign grouped_words = words | group_by_exp: "item", "item.english | slice: 0, 1" %}

{% for group in grouped_words %}
<h2 id="ek-{{ group.name }}">{{ group.name | upcase }}</h2>
{% assign english_terms = group.items | group_by: "english" %}
{% for english_term in english_terms %}
{% capture entry %}
{% assign first_word = english_term.items[0] %}
**{{ first_word.english }}** <br>
{% for def in english_term.items %}
{% assign other = "" %}
{% if def.other %}
{% assign other = ", " | append: def.other %}
{% endif %}
{% assign tumblr = "" %}
{% if def.tumblr %}
{% assign tumblr = " ([WotW entry](" | append: def.tumblr | append: "))" %}
{% endif %}
{% if def.pos == "noun" %}
{% capture secondline %}*(noun, {{ def.gender }}{{ other }})* - **{{ def.kolic }}** /{{ def.broad}}/ [{{def.narrow}}]{{ tumblr }}{% endcapture %}
{% elsif def.pos == "verb" %}
{% capture secondline %}*(verb, {{ def.transitivity }}{{ other }})* - **{{ def.kolic }}** /{{ def.broad}}/ [{{def.narrow}}]{{ tumblr }}{% endcapture %}
{% elsif def.pos == "adverb" %}
{% capture secondline %}*(adverb{{ other }})* - **{{ def.kolic }}** /{{ def.broad}}/ [{{def.narrow}}]{{ tumblr }}{% endcapture %}
{% elsif def.pos == "adjective" %}
{% capture secondline %}*(adjective{{ other }})* - **{{ def.kolic }}** /{{ def.broad}}/ [{{def.narrow}}]{{ tumblr }}{% endcapture %}
{% else %}
{% capture secondline %}*({{ def.pos }}{{ other }})* - **{{ def.kolic }}** /{{ def.broad}}/ [{{def.narrow}}]{{ tumblr }}{% endcapture %}
{% endif %}
&emsp;{{ forloop.index }}. {{ secondline }}<br>
{% if def.note %}
&emsp;&emsp;{{def.note}}<br>
{% endif %}
{% endfor %}
{% endcapture %}
{{ entry | strip_newlines }}
{% endfor %}
{% endfor %}

