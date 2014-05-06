
OpenSearch interface
====================

OpenSearch is a specification and a collection of technologies that allow publishing of search results in a format suitable for syndication and aggregation that can then be aggregated by larger indexes. It is a way for websites and search engines to publish search results in a standard and accessible format. It originates in a community effort built around Amazon's A9.com and is made available under the Creative Commons Attribution-Sharealike 2.5 license and it's now maintained in a community process at `opensearch.org <http://opensearch.org/>`_

The concept of OpenSearch is a simple format for specifying how to query a web resource (be it a search engine, catalogue, or registry environment) and additional metadata in the results to support syndicating these results. OpenSearch includes a description of how to query a given service and query the parameters supported.


OpenSearch Description Document
===============================

The OpenSearch Description Document is a XML document that defines the API, lists the result responses formats and used extensions allowing it to request specific and contextual query parameters for each dataset.

It includes the URL template element that shows clients how to make the requests.  For example, if a web site allows search by the URL:

 http://www.example.com?q=question

The OpenSearch description document provides a way to define where that search term goes. Essentially it looks like:

  http://www.example.com?q={searchTerms}

where {searchTerms} would be replaced by any general string.

This URL would be in the OpenSearch Description Url element as


<OpenSearchDescription  xmlns="http://a9.com/-/spec/opensearch/1.1/">
<ShortName>Data Search</ShortName>
<Description>
To use this service insert the search term required.
</Description>
<Url template="http://example.com/xml/?q={searchTerms?}" type="application/xhtml+xml"/>
</OpenSearchDescription>


The OpenSearch Description Documents can also lists other search result responses types for the same service. For example, if a given service also supports the output in JSON the OpenSearch description can be extended to

<OpenSearchDescription  xmlns="http://a9.com/-/spec/opensearch/1.1/">
<ShortName>Data Search</ShortName>
<Description>
To use this service insert the search term required.
</Description>
<Url template="http://example.com/xml/?q={searchTerms?}" type="application/xhtml+xml"/>
<Url template="http://example.com/json/?q={searchTerms?}"  type="application/json" />
</OpenSearchDescription>


OpenSearch does not mandate any particular type of response and can have any format represented by a MIME-type. Search clients can use OpenSearch description documents to learn about the interface of the service and select their fittest result encoding.

 



<OpenSearchDescription  xmlns="http://a9.com/-/spec/opensearch/1.1/">
<ShortName>Data Search</ShortName>
<Description>
A Dataset Series is a collection of products. To search for the desired Dataset by keyword tag or by any of the specific fields defined in the OpenSearch url.
</Description>
<Url template="http://example.com/json/?q={searchTerms?}&amp;
start_date={time:Start?}&amp;stop_date={time:End?}&amp;bbox={geo:box}"  type="application/json" />
<Url template="http://example.com/xml/?q={searchTerms?}&amp;
start_date={time:Start?}&amp;stop_date={time:End?}&amp;bbox={geo:box}" type="application/xhtml+xml"/>
<Url template="http://example.com/wtk/?q={searchTerms?}&amp;
start_date={time:Start?}&amp;stop_date={time:End?}&amp;bbox={geo:box}" type="application/wtk" />
</OpenSearchDescription>






<Url type="text/html" template="http://www.example.com?q={searchTerms}" />







OpenSearch Request
===================




OpenSearch Response
===================
The OpenSearch response elements can be used to extend existing syndication formats, such as RSS and Atom, with the extra metadata needed to return search results.





The OpenSearch description format allows the use of extensions that allow search engines to request a specific and contextual query parameter from search clients.
The flexibility of the OpenSearch protocol allows one to return lists of search results in any format that a client is capable of understanding. While Atom is common, search results in KML or JSON are equally possible. A JSON result set could be used to supply configuration options to a Javascript client such as OpenLayers, or provide the same search result set to a human-readable interface.
The OpenSearch Description Document includes a mandatory URL element containing a mandatory request template. Where several request templates are provided, a client may choose the one offering the most useful format (specified by MIME-type defined in the type attribute of the element). The following XML snippet illustrates a URL template suggesting a bounding box query for data, with results returned in KML:

<Url type="application/vnd.google-earth.kml+xml" template="http://acme.com/mykml?q={searchTerms} &amp;pw={startPage?}" />

This is a key feature of the description document that instructs a client application how to issue queries to the service. The URL template represents a parameterized form of the URL by which a search engine is queried. Each response format supported by the service needs its own distinct URL template included in the description. Note that for the given key-value pairs, the key can be an arbitrary string, specified by one given instance of an OpenSearch repository. For example, one service may provide a URL template asking for a q={searchTerms}, another might be configured to specify question={searchTerms}. It is the responsibility of the client applications to parse the URL template and create appropriate keys for each key-value pair. If a search engine wishes to express that a template parameter is optional and can be replaced with an empty string, then the “?” notation should be used. Specific services can extend the basic parameters included in the template (see next section).



We will use geospatial, temporal, earth observation and other suitable extensions to allow the definition of specific queriables. The OpenSearch protocol lists the different access points available for each result type (ATOM, GeoRSS, GeoJSON, Metalink, EOP/HMA, KML and HTML5) to allow the easy integration in other services and mash-up applications.
The Portal will use the OpenSearch description documents to learn about the public interface of a search climate data set. This description document will contain parameterized URL templates that indicate how the search client should make search requests. For example, if a web site allows search by the URL:
http://www.example.com?q=question
OpenSearch provides a way to define the template of that search URL. Essentially it looks like:
http://www.example.com?q={searchTerms}
where {searchTerms} would be replaced by any general string.
Furthermore, OpenSearch description format makes use of extensions that allow search engines to request a specific and contextual query parameter from search clients. For the World Bank Climate Change Knowledge Portal setting, the OpenSearch Geospatial and Temporal Extensions are used to express the parameters of spatial and temporal selection. So if the previous example was capable of explicitly searching for temporal and spatial range it would be defined as:
http://www.example.com?q={searchTerms}&s={time:start}&e={time:end}&bbox={geo:box}
In this case, the portal widget will fills in the search terms accordingly to the original user search, and creates a link to the resource’s data access.
