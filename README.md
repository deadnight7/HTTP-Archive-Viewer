HAR stands for [HTTP Archive format](http://www.softwareishard.com/blog/har-12-spec/). Browsers use
this format to export HTTP request and response traces as waterfal diagrams.

This repo contains a jQuery based widget to render HAR data as a waterfall diagram. I wrote this as
a lighter embeddable alternative to [Jan Odvarko](http://www.softwareishard.com/)'s online
[HAR Viewer](http://www.softwareishard.com/blog/har-viewer). In additon to supporting full
HAR-formatted JSON objects, this alternative can render requests and responses incrementally making
it suitable to show the waterfall lines as requests are being made.

This version also uses Steve Souder's
[draft conventions](http://stevesouders.com/misc/waterfall-ui.php) for connection state.

## Try Online

You can try this viewer online. Open
[http://s3u.github.com/har-view/](http://s3u.github.com/har-view/), and drop a HAR file anywhere in
the browser window.

## Example

![Example](https://github.com/s3u/har-view/raw/master/examples/sample.png)

## Prerquisites

Include the following to use this widget in a page.

    <script type='text/javascript' src='scripts/mustache.js'></script>
    <script type='text/javascript' src='scripts/jquery.min.js'></script>
    <script type='text/javascript' src='scripts/jquery-ui.min.js'></script>
    <script type='text/javascript' src='scripts/har-viewer.js'></script>
    <link rel='stylesheet' href='css/jquery-ui.css'/>
    <link rel='stylesheet' href='css/har-viewer.css'/>

Then place a div tag to hold the waterfall diagram.

    <div id='har-view'></div>

## Loading Full HAR Objects

If you have a full HAR object, you can initialize the diagram in one go.

    $('#har-view').HarView();
    var har = $('#har-view').data('HarView');
    har.render(data);

## Incremental Initialization

    $('#har-vew').HarView();
    var har = $('#har').data('HarView');

    // Add an entry - use a unique identifier for each request
    har.entry(id, {
        startedDateTime: t
    });

    // Add request data
    har.request(id, {
        method: 'GET',
        url: 'http://foo.com/blah',
        headers: [
            {name: 'Connection', value: 'keep-alive'}
            ]
        });

    // Add timings
    har.timings(id, {
                    "blocked": 100,
                    "dns": 10,
                    "connect": 20,
                    "send": 30,
                    "wait": 40,
                    "receive": 50
                });

    // Add response
    har.response(id, {
        "status": 200,
        "bodySize": 8730,
        "headers": [
            {
                "name": "content-type",
                "value": "text/xml; charset=utf-8"
            },
            {
                "name": "date",
                "value": "Tue, 27 Dec 2011 05:12:54 GMT"
            },
            {
                "name": "content-length",
                "value": "8730"
            },
            {
                "name": "connection",
                "value": "keep-alive"
            }
        ],
        "content": {
            "text": "<?xml version=\"1.0\" encoding=\"utf-8\" ?><?pageview_candidate?><SearchResponse xmlns=\"http://schemas.microsoft.com/LiveSearch/2008/04/XML/element\" Version=\"2.2\"><Query><SearchTerms>ql.io</SearchTerms></Query><web:Web xmlns:web=\"http://schemas.microsoft.com/LiveSearch/2008/04/XML/web\"><web:Total>9480000</web:Total><web:Offset>0</web:Offset><web:Results><web:WebResult><web:Title>Announcing ql.io � eBay Tech Blog</web:Title><web:Description>We are happy to announce ql.io � a declarative, evented, data-retrieval and aggregation gateway for HTTP APIs. Through ql.io, we want to help application developers ...</web:Description><web:Url>http://www.ebaytechblog.com/2011/11/30/announcing-ql-io/</web:Url><web:CacheUrl>http://cc.bingj.com/cache.aspx?q=%22ql+io%22&amp;d=4838852285236758&amp;w=d366d1bd,6816a241</web:CacheUrl><web:DisplayUrl>www.ebaytechblog.com/2011/11/30/announcing-ql-io</web:DisplayUrl><web:DateTime>2011-12-18T16:49:00Z</web:DateTime></web:WebResult><web:WebResult><web:Title>InfoQ: eBay Announces ql.io</web:Title><web:Description>We are happy to announce � a declarative, evented, data-retrieval and aggregation gateway for HTTP APIs. Through ql.io, we want to help application developers ...</web:Description><web:Url>http://www.infoq.com/news/2011/11/ql-io-release</web:Url><web:CacheUrl>http://cc.bingj.com/cache.aspx?q=%22ql+io%22&amp;d=4521484265719037&amp;w=75479e80,e3d1cb78</web:CacheUrl><web:DisplayUrl>www.infoq.com/news/2011/11/ql-io-release</web:DisplayUrl><web:DateTime>2011-12-19T20:56:00Z</web:DateTime></web:WebResult><web:WebResult><web:Title>ql.io</web:Title><web:Description>About ql.io A SQL and JSON inspired DSL. SQL is quite a powerful DSL to retrieve, filter, project, and join data � see efforts like A co-Relational Model of Data ...</web:Description><web:Url>http://ql.io/docs/about</web:Url><web:CacheUrl>http://cc.bingj.com/cache.aspx?q=%22ql+io%22&amp;d=4518031125644867&amp;w=74c43eab,dbf1bb</web:CacheUrl><web:DisplayUrl>ql.io/docs/about</web:DisplayUrl><web:DateTime>2011-12-21T10:29:00Z</web:DateTime></web:WebResult><web:WebResult><web:Title>Loading...</web:Title><web:Url>http://boiteaoutilsqsehse.com/?fp=DlOivWY6Bo5JgGGsWKkoyl6%2BrvNZEwke82VCseZGsYLvwDhb1klI42cDKEG8P6io0JiEZTZDujGpV4lR7mL5GQ%3D%3D&amp;prvtof=CixNAYdjuc66upUC%2B6ZKPNdSKwRl0fqF4hK%2F%2F38SPAQ%3D&amp;poru=ql%2FXWQYdGN72KZoJArBCCUi2lebzAsJhFQDcqdxcCD07gnbQ152YLanKi8KkNepG&amp;</web:Url><web:CacheUrl>http://cc.bingj.com/cache.aspx?q=%22ql+io%22&amp;d=4812498364402319&amp;w=70d5c13a,b15a48db</web:CacheUrl><web:DisplayUrl>boiteaoutilsqsehse.com</web:DisplayUrl><web:DateTime>2011-12-23T21:43:00Z</web:DateTime></web:WebResult><web:WebResult><web:Title>eBay&apos;s ql.io is an &quot;SQL&quot; for web APIs - The H Open Source: News ...</web:Title><web:Description>Inspired by SQL, eBay&apos;s ql.io allows complex mashups of web APIs to be expressed in a language which is automatically optimised for parallel execution</web:Description><web:Url>http://www.h-online.com/open/news/item/eBay-s-ql-io-is-an-SQL-for-web-APIs-1388806.html</web:Url><web:CacheUrl>http://cc.bingj.com/cache.aspx?q=%22ql+io%22&amp;d=4961486479494152&amp;w=2464a1ed,3a7bae99</web:CacheUrl><web:DisplayUrl>www.h-online.com/open/news/item/eBay-s-ql-io-is-an-SQL-for-web...</web:DisplayUrl><web:DateTime>2011-12-17T11:36:00Z</web:DateTime></web:WebResult><web:WebResult><web:Title>Manastirea Prislop Arsenie Boca - YouTube</web:Title><web:Description>Uploaded by portaltfm on Sep 26, 2010 no description available Category: Travel &amp; Events Tags: Manastirea Prislop Arsenie Boca License: Standard YouTube ...</web:Description><web:Url>http://www.youtube.com/watch?v=qL_Io-K9FHg</web:Url><web:CacheUrl>http://cc.bingj.com/cache.aspx?q=%22ql+io%22&amp;d=4612881174367018&amp;w=f8687101,70baa56</web:CacheUrl><web:DisplayUrl>www.youtube.com/watch?v=qL_Io-K9FHg</web:DisplayUrl><web:DateTime>2011-12-22T09:21:00Z</web:DateTime></web:WebResult><web:WebResult><web:Title>The Muffins salahkah ku - YouTube</web:Title><web:Description>Uploaded by lomangpanehh on May 11, 2009 no description available Category: People &amp; Blogs Tags: The Muffins salahkah ku License: Standard YouTube License ...</web:Description><web:Url>http://www.youtube.com/watch?v=Io9qL8G4-0s</web:Url><web:CacheUrl>http://cc.bingj.com/cache.aspx?q=%22ql+io%22&amp;d=4963711277532291&amp;w=b0713f61,eac926c8</web:CacheUrl><web:DisplayUrl>www.youtube.com/watch?v=Io9qL8G4-0s</web:DisplayUrl><web:DateTime>2011-12-22T20:25:00Z</web:DateTime></web:WebResult><web:WebResult><web:Title>Cephei.QL :: C++/CLI wrapper around QuantLib for F#</web:Title><web:Description>Cephei.QL is a library that wraps the QuantLib C++ library with classes that provide CTS interfaces that can be used from F#. Cephei.QL is not a simple wrapper that ...</web:Description><web:Url>http://ql.codeplex.com/</web:Url><web:CacheUrl>http://cc.bingj.com/cache.aspx?q=%22ql+io%22&amp;d=4533772184848168&amp;w=ca0af65d,3b42073b</web:CacheUrl><web:DisplayUrl>ql.codeplex.com</web:DisplayUrl><web:DateTime>2011-12-24T03:59:00Z</web:DateTime><web:SearchTags><web:WebSearchTag><web:Name>search.codeplex.project.name</web:Name><web:Value>&quot;QL&quot;</web:Value></web:WebSearchTag><web:WebSearchTag><web:Name>search.codeplex.project.title</web:Name><web:Value>&quot;Cephei.QL :: C++/CLI wrapper around QuantLib for F#&quot;</web:Value></web:WebSearchTag><web:WebSearchTag><web:Name>search.codeplex.project.description</web:Name><web:Value>&quot;Cephei.QL is a library that wraps the QuantLib C++ library with classes that provide CTS interfaces that can be used from F#. Cephei.QL is not a simple wrapper that stops at plumbing for P/Invoke type C functions that replicate Excel addin function.. Cephei.QL provides a high level interface that looks like a class library developed in a .NET language&quot;</web:Value></web:WebSearchTag><web:WebSearchTag><web:Name>search.codeplex.project.createddate</web:Name><web:Value>&quot;4/26/2011 2:23:21 AM&quot;</web:Value></web:WebSearchTag><web:WebSearchTag><web:Name>search.codeplex.project.projecttags</web:Name><web:Value>&quot;&quot;</web:Value></web:WebSearchTag><web:WebSearchTag><web:Name>search.codeplex.project.licenseshortname</web:Name><web:Value>&quot;Ms-RL&quot;</web:Value></web:WebSearchTag><web:WebSearchTag><web:Name>search.codeplex.project.currentreleasedate</web:Name><web:Value>&quot;5/13/2011 12:00:00 AM&quot;</web:Value></web:WebSearchTag><web:WebSearchTag><web:Name>search.codeplex.project.currentreleasedevelopmentstatus</web:Name><web:Value>&quot;Beta&quot;</web:Value></web:WebSearchTag><web:WebSearchTag><web:Name>search.codeplex.project.currentreleasename</web:Name><web:Value>&quot;2.101b&quot;</web:Value></web:WebSearchTag><web:WebSearchTag><web:Name>search.codeplex.project.currentreleaserating</web:Name><web:Value>&quot;0&quot;</web:Value></web:WebSearchTag><web:WebSearchTag><web:Name>search.codeplex.project.currentreleasenumberofratings</web:Name><web:Value>&quot;0&quot;</web:Value></web:WebSearchTag><web:WebSearchTag><web:Name>search.codeplex.project.currentreleasenumberofreviews</web:Name><web:Value>&quot;0&quot;</web:Value></web:WebSearchTag><web:WebSearchTag><web:Name>search.codeplex.project.downloadfilecount</web:Name><web:Value>&quot;0&quot;</web:Value></web:WebSearchTag><web:WebSearchTag><web:Name>search.codeplex.project.visitscount</web:Name><web:Value>&quot;6&quot;</web:Value></web:WebSearchTag><web:WebSearchTag><web:Name>search.codeplex.project.pageviewcount</web:Name><web:Value>&quot;13&quot;</web:Value></web:WebSearchTag><web:WebSearchTag><web:Name>search.codeplex.project.contributorscount</web:Name><web:Value>&quot;1&quot;</web:Value></web:WebSearchTag></web:SearchTags></web:WebResult><web:WebResult><web:Title>QL - Definition by AcronymFinder - Abbreviations and acronyms ...</web:Title><web:Description>sort results: alphabetical | rank ? Rank Abbr. Meaning ***** QL: Quick Look ***** QL: Queensland (Australia) ***** QL: Quality of Life (USAF funding issues)</web:Description><web:Url>http://www.acronymfinder.com/QL.html</web:Url><web:CacheUrl>http://cc.bingj.com/cache.aspx?q=%22ql+io%22&amp;d=4520011090495820&amp;w=d750a496,47fa3370</web:CacheUrl><web:DisplayUrl>www.acronymfinder.com/QL.html</web:DisplayUrl><web:DateTime>2011-12-23T07:41:00Z</web:DateTime></web:WebResult><web:WebResult><web:Title>QL-SHOP</web:Title><web:Description>QL-SHOP Watch!</web:Description><web:Url>http://ql-shop.com/</web:Url><web:CacheUrl>http://cc.bingj.com/cache.aspx?q=%22ql+io%22&amp;d=4675007874664093&amp;w=e9ef8dcb,594f76ca</web:CacheUrl><web:DisplayUrl>ql-shop.com</web:DisplayUrl><web:DateTime>2011-12-22T21:12:00Z</web:DateTime></web:WebResult></web:Results></web:Web></SearchResponse>"
        }
    });

See examples/index.html for a working example.

