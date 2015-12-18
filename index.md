---
layout: home
permalink: /
image:
  feature: sample-image-1.jpg
---

<div class="tiles">

<div class="tile">
  <h2 class="post-title">VnmrJ is now Open Source!</h2>
  <p class="post-excerpt">VnmrJ has been released as open source software under the name OpenVnmrJ.</p>
</div><!-- /.tile -->

<div class="tile">
  <h2 class="post-title">Download the Latest Release</h2>
  <p class="post-excerpt"><a href="{{site.baseurl}}Downloading/">Download</a> and install the latest release of OpenVnmrJ</p>
</div><!-- /.tile -->

<div class="tile">
  <h2 class="post-title">Contribute</h2>
  <p class="post-excerpt">Learn how to <a href="{{site.baseurl}}Contributing/">contribute</a> documentation, pulse sequences, macros, or other code to OpenVnmrJ.</p>
</div><!-- /.tile -->

<div class="tile">
  <h2 class="post-title">Support</h2>
<p class="post-excerpt"><a href="http://spinsights.chem.agilent.com">Connect</a> with the <a href="https://spinsights.chem.agilent.com">Spinsights</a> community to ask questions and get help with VnmrJ and OpenVnmrJ.</p>
</div><!-- /.tile -->

</div><!-- /.tiles -->
<div class="tiles">
{% for post in site.posts %}
	{% include post-grid.html %}
{% endfor %}
