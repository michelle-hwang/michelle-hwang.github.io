---
title: Projects
layout: splash
permalink: /projects/
intro:
  - exerpt: "Intro text here"
    type: "center"
feature_row:
  - image_path:
    alt: "placeholder image 1"
    title: "placeholder 1"
    excerpt: "lalalalalala"
  - image_path:
    alt: "placeholder image 2"
    title: "placedoler 2"
  - image_path:
    alt: "placeholder image 3"
    title: "placeholder 3"
feature_row2:
  - image_path:
    alt:
    title: left
    url: "#test-link"
    btn_label: "Read More"
    btn_class: "btn--inverse"
    type: left
feature_row3:
  - image_path:
    alt:
    title: right
    url: "#test-link"
    btn_label: "Read More"
    btn_class: "btn--inverse"
    type: right
feature_row4:
  - image_path:
    alt:
    title: middle
    url: "#test-link"
    btn_label: "Read More"
    btn_class: "btn--inverse"
    type: center
---

{% include feature_row id="intro" type="center" %}

{% include feature_row %}

{% include feature_row id="feature_row2" type="left" %}

{% include feature_row id="feature_row3" type="right" %}

{% include feature_row id="feature_row4" type="center" %}
