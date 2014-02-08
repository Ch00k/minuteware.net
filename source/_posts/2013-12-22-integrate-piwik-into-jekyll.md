---
layout: post
title:  "Integrate Piwik into Jekyll"
date:   2013-12-22 12:01:01
comments: true
categories: discoveries
tags: piwik jekyll
---


First we have to take the [Piwik](http://piwik.org/) JavaScript Tracking Code from Piwik Administration website and replace Piwik URL and site ID with Jekyll variables, like so (note the `{% raw %}{{ site.piwik.base_url }}{% endraw %}` and `{% raw %}{{ site.piwik.site_id }}{% endraw %}`):

```html
<!-- Piwik -->
<script type="text/javascript">
  var _paq = _paq || [];
  _paq.push(["trackPageView"]);
  _paq.push(["enableLinkTracking"]);

  (function() {
    var u=(("https:" == document.location.protocol) ? "https" : "http") + "://{% raw %}{{ site.piwik.base_url }}{% endraw %}/";
    _paq.push(["setTrackerUrl", u+"piwik.php"]);
    _paq.push(["setSiteId", "{% raw %}{{ site.piwik.site_id }}{% endraw %}"]);
    var d=document, g=d.createElement("script"), s=d.getElementsByTagName("script")[0]; g.type="text/javascript";
    g.defer=true; g.async=true; g.src=u+"piwik.js"; s.parentNode.insertBefore(g,s);
  })();
</script>
<!-- End Piwik Code -->
```

Save this code snippet as `_includes/piwik`

Now we need `base_url` and `site_id` variables defined in `_config.yml`. Add the following to `_config.yml`:

```yaml
piwik:
  base_url: piwik.mydomain.net
  site_id: 1
```

For the default Jekyll template add the following after `</head>` tag in `_layouts/default.html`:

```
{% raw %}{% include piwik %}{% endraw %}
```

That's it. After our website is rebuilt all the pages will include the above Piwik JS tracking code with variables replaced with their values from _config.yml
