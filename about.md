---
layout: page
title: About
permalink: about/
---

<style>
    #map_canvas {
        width: 600px;
		height: 400px;
	}
</style>
<script src="https://maps.googleapis.com/maps/api/js"></script>
<script>
    function initialize() {
		var myLatLong = new google.maps.LatLng(-38.151919, 144.3663201);
        var mapCanvas = document.getElementById('map_canvas');
        var mapOptions = {
          center: myLatLong,
          zoom: 14,
          mapTypeId: google.maps.MapTypeId.ROADMAP
        }
        var map = new google.maps.Map(mapCanvas, mapOptions)
		var marker = new google.maps.Marker({
			position: myLatLong,
			map: map,
			title: 'Hello World!'
		});

	}
	google.maps.event.addDomListener(window, 'load', initialize);
</script>


<!-- <p class="message"> -->
<!--   Hey there! This page is included as an example. Feel free to customize it for -->
<!--   your own use upon downloading. Carry on! -->
<!-- </p> -->

I am a biostatistician within the Research Directorate at Barwon Health,
Geelong, Australia.

The views expressed on this website are solely my own, and do not necessarily reflect those of my employer.

<div id="map_canvas"></div>

### About this website

This website is built upon Poole, which is built upon
[Jekyll](http://jekyllrb.com). It's made by
[@mdo](https://twitter.com/mdo). Credit where credit's due, you can find more
information at [GitHub](https://github.com/poole).
