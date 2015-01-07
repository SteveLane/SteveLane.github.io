---
layout: post
title: "Research Week highlights"
galleryid: research-week-2014
comments: true
customjs:
 - /public/js/jquery-1.11.0.min.js
 - /public/js/lightbox.min.js
tags: research-week poster-competition
---

<!-- <script src="{{site.baseurl}}public/js/jquery-1.10.2.min.js"></script> -->
<!-- <script src="{{site.baseurl}}public/js/lightbox-2.6.min.js"></script> -->
<!-- <link href="{{site.baseurl}}public/css/lightbox.css" rel="stylesheet" /> -->
<!-- <link href="{{site.baseurl}}public/css/gallery-grid.css" rel="stylesheet" /> -->

On Monday 10th Nov Barwon Health Research Week was launched with a keynote
speech address by Professor Terry Speed
([Walter and Eliza Hall Institute of Medical Research](http://www.wehi.edu.au/people/terry-speed),
Melbourne) who is a recent Eureka Prize winner for science engagement. Terry
gave an informative and entertaining talk to a large crowd on the topic of
epigenetics.

The popular Barwon Health Research Week Poster competition culminated on
Wednesday with prize giving and celebrations (winners are highlighted below) and
the new Chair of Orthopaedics, Professor Richard Page. Richard gave us a
personal look at his achievements in his inaugural professorial address "Big
Data".

The Smart Geelong Network 'Researcher of the Year' prize was awarded to
Associate Professor Bronwyn Fox who leads the carbon fibre and composite
research team in the
[Institute for Frontier Materials](http://www.carbonnexus.com.au/index.php/the-people/executive-team/5-associate-professor-bronwyn-fox).

<!-- taken from http://alijafarian.com/responsive-image-grids-using-css/ -->
<div>
{% for gallery in site.data.research-week-2014-gallery %}
  {% if gallery.id == page.galleryid %}
	<ul class="rig columns-3">
    {% for image in gallery.images %}
      <li>
        <a href="{{ gallery.imagefolder }}/{{ image.name }}" data-lightbox="{{ gallery.id }}" title="{{ image.title }}">
          <img src="{{ gallery.imagefolder }}/{{ image.thumb }}">
        </a>
		{{ image.text }}
      </li>
    {% endfor %}
    </ol>
  {% endif %}
{% endfor %}
</div>
