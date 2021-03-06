---
vim:	ts=3
---

# Embedding MEI #

In addition to Humdrum data, MEI files can be embedded in the 
webpage (or loaded from an external URL).  In general doing this is slower since 
an extra conversion into Humdrum is needed, and MEI files
are about 20 times larger than Humdrum data for the same score.  The <nobr>30-measure</nobr>
example on this page is 216 KB, while the Humdrum data is 12 KB.

You can also <a target="_blank"
href="http://doc.verovio.humdrum.org/interface/mei/">drag-and-drop a
MEI file</a> into <a target="_blank"
href="http://verovio.humdrum.org">Verovio Humdrum Viewer</a> to
convert to Humdrum, and then paste the Humdrum conversion into your
webpage, rather than converting the XML data files on the fly to
Humdrum data.

MEI content can be embedded into the webpage in place of Humdrum
data.  When the plugin reads the Humdrum script element and sees
MEI instead of Humdrum data, it will convert it automatically
into Humdrum before proceeding to generate notation.

The following example starts with MEI data, and then converts
internally to Humdrum data before generating graphical notation.
Scroll through the following box to view all of the MEI content
enclosed in the Humdrum script element:

<div class="scrolling"></div>
``` html
{% include_relative trinklied.txt %}
```

{% include_relative trinklied.txt %}


Here is the converted Humdrum data:

<div class="scrolling"></div>
``` html
{% include_relative Mendelssohn_Op75_3.krn -%}
```


# MEI from URL #

The MEI data for the example song was taken from <a target="_blank"
href="http://www3.cpdl.org/wiki/index.php/Trinklied,_Op._75,_No._3_(Felix_Mendelssohn)">CPDL
#52575</a>.  In this case the MEI data file linked to on that
page is in a compressed format, so it cannot be loaded directly with the Humdrum notation plugin.
First it must be downloaded and unzipped to extract the uncompressed MEI datafile.

Here is the same music loaded from a URL coming from the same
location as this webpage rather than stored directly inside of the
webpage:

``` html
{% include_relative trinklied-url.txt %}
```

{% include_relative trinklied-url.txt %}

The full address of the url is <a target="_blank" href="https://plugin.humdrum.org/topic/mei/Mendelssohn_Op75_3.mei">https://plugin.humdrum.org/topic/mei/Mendelssohn_Op75_3.mei</a>.


Note that filter commands can be added even when the input data is
MEI.  The data is converted automatically into Humdrum data,
and then the filter line is added to the Humdrum data before being
rendered into graphical music notation.  The filter pipe-line for
this example means:

|  Command&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  |  Options&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;       | Meaning
|-----------|----------------|--------
| myank     | -m&nbsp;0-5    | yank the first five measures of the music (0 means include the pickup-measure)
| extract   | -i&nbsp;kern   | keep only the kern data spines (getting rid of lyrics and dynamics)
| autobeam  |                | automatically beam the music by quarter notes (due to the 3/4 meter)
| transpose | -b&nbsp;5      | transpose music up a minor second (base-40 interval-class 5)
| satb2gs   |                | convert SATB system into a grand-staff system

<script>
document.addEventListener("DOMContentLoaded", function() {
	var list = document.querySelectorAll("div.scrolling");
	for (var i=0; i<list.length; i++) {
		var element = list[i].nextElementSibling;
		if (element) {
			list[i].innerHTML = element.outerHTML;
			element.style.display = "none";
		}
	}
});
</script>


{% comment %}
	The following data is used to print some music in the header of this page.
	The include file _includes/music-banner.html reads this data and creates
	the notation in the header.  If there is a !!!title: record in the
	Humdrum data below, then it will be placed above the musical example.
{% endcomment %}

<script type="text/x-humdrum" id="title-notation-source">
!!!title: <a target="_blank" href="http://www3.cpdl.org/wiki/index.php/Trinklied,_Op._75,_No._3_(Felix_Mendelssohn)">Mendelssohn: Trinklied, op. 75, no. 3, Bass 2 part</a>
{% include_relative Mendelssohn_Op75_3.krn -%}
!!!filter: extract -k 1
</script>
