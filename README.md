PHP Sitemap Generator
=====================

This class can be used to generate sitemaps.

Internally uses SplFixedArrays, thus is faster and uses less memory.

Features:
* Follows [sitemaps.org](https://sitemaps.org/) protocol
* Supports alternative links for multi-language pages (see [google docs](https://webmasters.googleblog.com/2012/05/multilingual-and-multinational-site.html))
* toString method returns sitemap's XML text
* all vars and methods have public or protected (not private) member access to simplify inheritance

Usage example:

```php
<?php

include "src/SitemapGenerator.php";

$generator = new \SeeKing\SitemapGenerator\SitemapGenerator('example.com');

// will create also compressed (gzipped) sitemap
$generator->createGZipFile = true;

// determine how many urls should be put into one file
// according to standard protocol 50000 is maximum value (see http://www.sitemaps.org/protocol.html)
$generator->maxURLsPerSitemap = 50000;

// sitemap file name
$generator->sitemapFileName = "sitemap.xml";

// sitemap index file name
$generator->sitemapIndexFileName = "sitemap-index.xml";

// alternate languages
$alternates = [
    ['hreflang' => 'de', 'href' => "http://www.example.com/de"],
    ['hreflang' => 'fr', 'href' => "http://www.example.com/fr"],
];

// adding url `loc`, `lastmodified`, `changefreq`, `priority`, `alternates`
$generator->addUrl('http://example.com/url/path/', new DateTime(), 'always', '0.5', $alternates);

// generating internally a sitemap
$generator->createSitemap();

// outputting the XML to screen
echo $generator->toString();

// writing early generated sitemap to file
$generator->writeSitemap();
```

Inspired by @pawelantczak.