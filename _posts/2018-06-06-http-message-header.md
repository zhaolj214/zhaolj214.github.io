---
layout: post
title:  "HTTP message header"
categories: HTTP
tags: HTTP
author: 若水三千
---

* content
{:toc}


 **Message Headers** 

<dl>
    <dt>Last Updated</dt>
    <dd>2018-07-13</dd>
</dl>

#### Permanent Message Header Field Names ####

<dl>
    <dt>Registration Procedure(s)</dt>
    <dd>
        <pre>Expert Review</pre>
    </dd>
    <dt>Expert(s)</dt>
    <dd>
        <pre>Graham Klyne</pre>
    </dd>
    <dt>Reference</dt>
    <dd>[<a href="https://tools.ietf.org/html/rfc3864">RFC3864</a>]</dd>
    <dt>Note</dt>
    <dd>
        <pre>[<a href="https://tools.ietf.org/html/rfc5504">RFC5504</a>] specified that no new header fields be registered that begin with "Downgraded-". 
That restriction is now lifted, per [<a href="https://tools.ietf.org/html/rfc6857">RFC6857</a>].</pre>
    </dd>
    <dt>Note</dt>
    <dd>
        <pre>See section 8.3.1 of [<a href="https://tools.ietf.org/html/rfc7231">RFC7231</a>] for information on registering new HTTP Header Fields.</pre>
    </dd>
    <dd></dd>
</dl>
 
<table id="table-perm-headers" class="sortable">
    <thead>
        <tr style="cursor: pointer;">
            <td>Header Field Name</td>
            <td>Template</td>
            <td>Protocol</td>
            <td>Status</td>
            <td>Reference</td>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>A-IM</td>
            <td></td>
            <td>http</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4229">RFC4229</a>]</td>
        </tr>
        <tr>
            <td>Accept</td>
            <td></td>
            <td>http</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc7231">RFC7231, Section 5.3.2</a>]</td>
        </tr>
        <tr>
            <td>Accept-Additions</td>
            <td></td>
            <td>http</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4229">RFC4229</a>]</td>
        </tr>
        <tr>
            <td>Accept-Charset</td>
            <td></td>
            <td>http</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc7231">RFC7231, Section 5.3.3</a>]</td>
        </tr>
        <tr>
            <td>Accept-Datetime</td>
            <td></td>
            <td>http</td>
            <td>informational</td>
            <td>[<a href="https://tools.ietf.org/html/rfc7089">RFC7089</a>]</td>
        </tr>
        <tr>
            <td>Accept-Encoding</td>
            <td></td>
            <td>http</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc7231">RFC7231, Section 5.3.4</a>][<a href="https://tools.ietf.org/html/rfc7694">RFC7694, Section 3</a>]</td>
        </tr>
        <tr>
            <td>Accept-Features</td>
            <td></td>
            <td>http</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4229">RFC4229</a>]</td>
        </tr>
        <tr>
            <td>Accept-Language</td>
            <td></td>
            <td>http</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc7231">RFC7231, Section 5.3.5</a>]</td>
        </tr>
        <tr>
            <td>Accept-Language</td>
            <td></td>
            <td>mail</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4021">RFC4021</a>]</td>
        </tr>
        <tr>
            <td>Accept-Patch</td>
            <td></td>
            <td>http</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc5789">RFC5789</a>]</td>
        </tr>
        <tr>
            <td>Accept-Post</td>
            <td>
            <a href="perm/accept-post">perm/accept-post</a>
            </td>
            <td>http</td>
            <td>standard</td>
            <td>[<a href="https://www.w3.org/TR/ldp/">https://www.w3.org/TR/ldp/</a>]</td>
        </tr>
        <tr>
            <td>Accept-Ranges</td>
            <td></td>
            <td>http</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc7233">RFC7233, Section 2.3</a>]</td>
        </tr>
        <tr>
            <td>Age</td>
            <td></td>
            <td>http</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc7234">RFC7234, Section 5.1</a>]</td>
        </tr>
        <tr>
                <td>Allow</td>
                <td></td>
                <td>http</td>
                <td>standard</td>
                <td>[<a href="https://tools.ietf.org/html/rfc7231">RFC7231, Section 7.4.1</a>]</td>
        </tr>
        <tr>
            <td>ALPN</td>
            <td></td>
            <td>http</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc7639">RFC7639, Section 2</a>]</td>
        </tr>
        <tr>
            <td>Also-Control</td>
            <td></td>
            <td>netnews</td>
            <td>obsoleted</td>
            <td>[<a href="https://tools.ietf.org/html/rfc1849">RFC1849</a>][<a href="https://tools.ietf.org/html/rfc5536">RFC5536</a>]</td>
        </tr>
        <tr>
            <td>Alt-Svc</td>
            <td></td>
            <td>http</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc7838">RFC7838</a>]</td>
        </tr>
        <tr>
            <td>Alt-Used</td>
            <td></td>
            <td>http</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc7838">RFC7838</a>]</td>
        </tr>
        <tr>
            <td>Alternate-Recipient</td>
            <td></td>
            <td>mail</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4021">RFC4021</a>]</td>
        </tr>
        <tr>
            <td>Alternates</td>
            <td></td>
            <td>http</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4229">RFC4229</a>]</td>
        </tr>
        <tr>
            <td>Apply-To-Redirect-Ref</td>
            <td></td>
            <td>http</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4437">RFC4437</a>]</td>
        </tr>
        <tr>
            <td>Approved</td>
            <td></td>
            <td>netnews</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc5536">RFC5536</a>]</td>
        </tr>
        <tr>
            <td>Archive</td>
            <td></td>
            <td>netnews</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc5536">RFC5536</a>]</td>
        </tr>
        <tr>
            <td>Archived-At</td>
            <td></td>
            <td>mail</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc5064">RFC5064</a>]</td>
        </tr>
        <tr>
            <td>Archived-At</td>
            <td></td>
            <td>netnews</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc5064">RFC5064</a>]</td>
        </tr>
        <tr>
            <td>Article-Names</td>
            <td></td>
            <td>netnews</td>
            <td>obsoleted</td>
            <td>[<a href="https://tools.ietf.org/html/rfc1849">RFC1849</a>][<a href="https://tools.ietf.org/html/rfc5536">RFC5536</a>]</td>
        </tr>
        <tr>
            <td>Article-Updates</td>
            <td></td>
            <td>netnews</td>
            <td>obsoleted</td>
            <td>[<a href="https://tools.ietf.org/html/rfc1849">RFC1849</a>][<a href="https://tools.ietf.org/html/rfc5536">RFC5536</a>]</td>
        </tr>
        <tr>
            <td>Authentication-Control</td>
            <td></td>
            <td>http</td>
            <td>experimental</td>
            <td>[<a href="https://tools.ietf.org/html/rfc8053">RFC8053, Section 4</a>]</td>
        </tr>
        <tr>
            <td>Authentication-Info</td>
            <td></td>
            <td>http</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc7615">RFC7615, Section 3</a>]</td>
        </tr>
        <tr>
            <td>Authentication-Results</td>
            <td></td>
            <td>mail</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc7601">RFC7601</a>]</td>
        </tr>
        <tr>
            <td>Authorization</td>
            <td></td>
            <td>http</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc7235">RFC7235, Section 4.2</a>]</td>
        </tr>
        <tr>
            <td>Auto-Submitted</td>
            <td></td>
            <td>mail</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc3834">RFC3834 section 5</a>]</td>
        </tr>
        <tr>
            <td>Autoforwarded</td>
            <td></td>
            <td>mail</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4021">RFC4021</a>]</td>
        </tr>
        <tr>
            <td>Autosubmitted</td>
            <td></td>
            <td>mail</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4021">RFC4021</a>]</td>
        </tr>
        <tr>
            <td>Base</td>
            <td></td>
            <td>MIME</td>
            <td>obsoleted</td>
            <td>[<a href="https://tools.ietf.org/html/rfc1808">RFC1808</a>][<a href="https://tools.ietf.org/html/rfc2068">RFC2068 Section 14.11</a>]</td>
        </tr>
        <tr>
            <td>Bcc</td>
            <td></td>
            <td>mail</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc5322">RFC5322</a>]</td>
        </tr>
        <tr>
            <td>Body</td>
            <td></td>
            <td>none</td>
            <td>reserved</td>
            <td>[<a href="https://tools.ietf.org/html/rfc6068">RFC6068</a>]</td>
        </tr>
        <tr>
            <td>C-Ext</td>
            <td></td>
            <td>http</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4229">RFC4229</a>]</td>
        </tr>
        <tr>
            <td>C-Man</td>
            <td></td>
            <td>http</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4229">RFC4229</a>]</td>
        </tr>
        <tr>
            <td>C-Opt</td>
            <td></td>
            <td>http</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4229">RFC4229</a>]</td>
        </tr>
        <tr>
            <td>C-PEP</td>
            <td></td>
            <td>http</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4229">RFC4229</a>]</td>
        </tr>
        <tr>
            <td>C-PEP-Info</td>
            <td></td>
            <td>http</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4229">RFC4229</a>]</td>
        </tr>
        <tr>
            <td>Cache-Control</td>
            <td></td>
            <td>http</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc7234">RFC7234, Section 5.2</a>]</td>
        </tr>
        <tr>
            <td>CalDAV-Timezones</td>
            <td></td>
            <td>http</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc7809">RFC7809, Section 7.1</a>]</td>
        </tr>
        <tr>
            <td>Cancel-Key</td>
            <td></td>
            <td>netnews</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc8315">RFC8315</a>]</td>
        </tr>
        <tr>
            <td>Cancel-Lock</td>
            <td></td>
            <td>netnews</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc8315">RFC8315</a>]</td>
        </tr>
        <tr>
            <td>Cc</td>
            <td></td>
            <td>mail</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc5322">RFC5322</a>]</td>
        </tr>
        <tr>
            <td>Close</td>
            <td></td>
            <td>http</td>
            <td>reserved</td>
            <td>[<a href="https://tools.ietf.org/html/rfc7230">RFC7230, Section 8.1</a>]</td>
        </tr>
        <tr>
            <td>Comments</td>
            <td></td>
            <td>mail</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc5322">RFC5322</a>]</td>
        </tr>
        <tr>
            <td>Comments</td>
            <td></td>
            <td>netnews</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc5536">RFC5536</a>][<a href="https://tools.ietf.org/html/rfc5322">RFC5322</a>]</td>
        </tr>
        <tr>
            <td>Connection</td>
            <td></td>
            <td>http</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc7230">RFC7230, Section 6.1</a>]</td>
        </tr>
        <tr>
            <td>Content-Alternative</td>
            <td></td>
            <td>MIME</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4021">RFC4021</a>]</td>
        </tr>
        <tr>
            <td>Content-Base</td>
            <td></td>
            <td>http</td>
            <td>obsoleted</td>
            <td>[<a href="https://tools.ietf.org/html/rfc2068">RFC2068</a>][<a href="https://tools.ietf.org/html/rfc2616">RFC2616</a>]</td>
        </tr>
        <tr>
            <td>Content-Base</td>
            <td></td>
            <td>MIME</td>
            <td>obsoleted</td>
            <td>[<a href="https://tools.ietf.org/html/rfc2110">RFC2110</a>][<a href="https://tools.ietf.org/html/rfc2557">RFC2557</a>]</td>
        </tr>
        <tr>
            <td>Content-Description</td>
            <td></td>
            <td>MIME</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4021">RFC4021</a>]</td>
        </tr>
        <tr>
            <td>Content-Disposition</td>
            <td></td>
            <td>http</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc6266">RFC6266</a>]</td>
        </tr>
        <tr>
            <td>Content-Disposition</td>
            <td></td>
            <td>MIME</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4021">RFC4021</a>]</td>
        </tr>
        <tr>
            <td>Content-Duration</td>
            <td></td>
            <td>MIME</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4021">RFC4021</a>]</td>
        </tr>
        <tr>
            <td>Content-Encoding</td>
            <td></td>
            <td>http</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc7231">RFC7231, Section 3.1.2.2</a>]</td>
        </tr>
        <tr>
            <td>Content-features</td>
            <td></td>
            <td>MIME</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4021">RFC4021</a>]</td>
        </tr>
        <tr>
            <td>Content-ID</td>
            <td></td>
            <td>http</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4229">RFC4229</a>]</td>
        </tr>
        <tr>
            <td>Content-ID</td>
            <td></td>
            <td>MIME</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4021">RFC4021</a>]</td>
        </tr>
        <tr>
            <td>Content-Identifier</td>
            <td></td>
            <td>mail</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4021">RFC4021</a>]</td>
        </tr>
        <tr>
            <td>Content-Language</td>
            <td></td>
            <td>http</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc7231">RFC7231, Section 3.1.3.2</a>]</td>
        </tr>
        <tr>
            <td>Content-Language</td>
            <td></td>
            <td>MIME</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4021">RFC4021</a>]</td>
        </tr>
        <tr>
            <td>Content-Length</td>
            <td></td>
            <td>http</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc7230">RFC7230, Section 3.3.2</a>]</td>
        </tr>
        <tr>
            <td>Content-Location</td>
            <td></td>
            <td>http</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc7231">RFC7231, Section 3.1.4.2</a>]</td>
        </tr>
        <tr>
            <td>Content-Location</td>
            <td></td>
            <td>MIME</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4021">RFC4021</a>]</td>
        </tr>
        <tr>
            <td>Content-MD5</td>
            <td></td>
            <td>http</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4229">RFC4229</a>]</td>
        </tr>
        <tr>
            <td>Content-MD5</td>
            <td></td>
            <td>MIME</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4021">RFC4021</a>]</td>
        </tr>
        <tr>
            <td>Content-Range</td>
            <td></td>
            <td>http</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc7233">RFC7233, Section 4.2</a>]</td>
        </tr>
        <tr>
            <td>Content-Return</td>
            <td></td>
            <td>mail</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4021">RFC4021</a>]</td>
        </tr>
        <tr>
            <td>Content-Script-Type</td>
            <td></td>
            <td>http</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4229">RFC4229</a>]</td>
        </tr>
        <tr>
            <td>Content-Style-Type</td>
            <td></td>
            <td>http</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4229">RFC4229</a>]</td>
        </tr>
        <tr>
            <td>Content-Transfer-Encoding</td>
            <td></td>
            <td>MIME</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4021">RFC4021</a>]</td>
        </tr>
        <tr>
            <td>Content-Translation-Type</td>
            <td></td>
            <td>MIME</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc8255">RFC8255</a>]</td>
        </tr>
        <tr>
            <td>Content-Type</td>
            <td></td>
            <td>http</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc7231">RFC7231, Section 3.1.1.5</a>]</td>
        </tr>
        <tr>
            <td>Content-Type</td>
            <td></td>
            <td>MIME</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4021">RFC4021</a>]</td>
        </tr>
        <tr>
            <td>Content-Version</td>
            <td></td>
            <td>http</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4229">RFC4229</a>]</td>
        </tr>
        <tr>
            <td>Control</td>
            <td></td>
            <td>netnews</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc5536">RFC5536</a>]</td>
        </tr>
        <tr>
            <td>Conversion</td>
            <td></td>
            <td>mail</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4021">RFC4021</a>]</td>
        </tr>
        <tr>
            <td>Conversion-With-Loss</td>
            <td></td>
            <td>mail</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4021">RFC4021</a>]</td>
        </tr>
        <tr>
            <td>Cookie</td>
            <td></td>
            <td>http</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc6265">RFC6265</a>]</td>
        </tr>
        <tr>
            <td>Cookie2</td>
            <td></td>
            <td>http</td>
            <td>obsoleted</td>
            <td>[<a href="https://tools.ietf.org/html/rfc2965">RFC2965</a>][<a href="https://tools.ietf.org/html/rfc6265">RFC6265</a>]</td>
        </tr>
        <tr>
            <td>DASL</td>
            <td></td>
            <td>http</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc5323">RFC5323</a>]</td>
        </tr>
        <tr>
            <td>DAV</td>
            <td></td>
            <td>http</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc4918">RFC4918</a>]</td>
        </tr>
        <tr>
            <td>DL-Expansion-History</td>
            <td></td>
            <td>mail</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4021">RFC4021</a>]</td>
        </tr>
        <tr>
            <td>Date</td>
            <td></td>
            <td>http</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc7231">RFC7231, Section 7.1.1.2</a>]</td>
        </tr>
        <tr>
            <td>Date</td>
            <td></td>
            <td>mail</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc5322">RFC5322</a>]</td>
        </tr>
        <tr>
            <td>Date</td>
            <td></td>
            <td>netnews</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc5536">RFC5536</a>][<a href="https://tools.ietf.org/html/rfc5322">RFC5322</a>]</td>
        </tr>
        <tr>
            <td>Date-Received</td>
            <td></td>
            <td>netnews</td>
            <td>obsoleted</td>
            <td>[<a href="https://tools.ietf.org/html/rfc0850">RFC0850</a>][<a href="https://tools.ietf.org/html/rfc5536">RFC5536</a>]</td>
        </tr>
        <tr>
            <td>Default-Style</td>
            <td></td>
            <td>http</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4229">RFC4229</a>]</td>
        </tr>
        <tr>
            <td>Deferred-Delivery</td>
            <td></td>
            <td>mail</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4021">RFC4021</a>]</td>
        </tr>
        <tr>
            <td>Delivery-Date</td>
            <td></td>
            <td>mail</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4021">RFC4021</a>]</td>
        </tr>
        <tr>
            <td>Delta-Base</td>
            <td></td>
            <td>http</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4229">RFC4229</a>]</td>
        </tr>
        <tr>
            <td>Depth</td>
            <td></td>
            <td>http</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc4918">RFC4918</a>]</td>
        </tr>
        <tr>
            <td>Derived-From</td>
            <td></td>
            <td>http</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4229">RFC4229</a>]</td>
        </tr>
        <tr>
            <td>Destination</td>
            <td></td>
            <td>http</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc4918">RFC4918</a>]</td>
        </tr>
        <tr>
            <td>Differential-ID</td>
            <td></td>
            <td>http</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4229">RFC4229</a>]</td>
        </tr>
        <tr>
            <td>Digest</td>
            <td></td>
            <td>http</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4229">RFC4229</a>]</td>
        </tr>
        <tr>
            <td>Discarded-X400-IPMS-Extensions</td>
            <td></td>
            <td>mail</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4021">RFC4021</a>]</td>
        </tr>
        <tr>
            <td>Discarded-X400-MTS-Extensions</td>
            <td></td>
            <td>mail</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4021">RFC4021</a>]</td>
        </tr>
        <tr>
            <td>Disclose-Recipients</td>
            <td></td>
            <td>mail</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4021">RFC4021</a>]</td>
        </tr>
        <tr>
            <td>Disposition-Notification-Options</td>
            <td></td>
            <td>mail</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4021">RFC4021</a>]</td>
        </tr>
        <tr>
            <td>Disposition-Notification-To</td>
            <td></td>
            <td>mail</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4021">RFC4021</a>]</td>
        </tr>
        <tr>
            <td>Distribution</td>
            <td></td>
            <td>netnews</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc5536">RFC5536</a>]</td>
        </tr>
        <tr>
            <td>DKIM-Signature</td>
            <td></td>
            <td>mail</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc6376">RFC6376</a>]</td>
        </tr>
        <tr>
            <td>Downgraded-Bcc</td>
            <td></td>
            <td>mail</td>
            <td>obsoleted</td>
            <td>[<a href="https://tools.ietf.org/html/rfc5504">RFC5504</a>][<a href="https://tools.ietf.org/html/rfc6857">RFC6857</a>]</td>
        </tr>
        <tr>
            <td>Downgraded-Cc</td>
            <td></td>
            <td>mail</td>
            <td>obsoleted</td>
            <td>[<a href="https://tools.ietf.org/html/rfc5504">RFC5504</a>][<a href="https://tools.ietf.org/html/rfc6857">RFC6857</a>]</td>
        </tr>
        <tr>
            <td>Downgraded-Disposition-Notification-To</td>
            <td></td>
            <td>mail</td>
            <td>obsoleted</td>
            <td>[<a href="https://tools.ietf.org/html/rfc5504">RFC5504</a>][<a href="https://tools.ietf.org/html/rfc6857">RFC6857</a>]</td>
        </tr>
        <tr>
            <td>Downgraded-Final-Recipient</td>
            <td></td>
            <td>mail</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc6857">RFC6857 Section 3.1.10</a>]</td>
        </tr>
        <tr>
            <td>Downgraded-From</td>
            <td></td>
            <td>mail</td>
            <td>obsoleted</td>
            <td>[<a href="https://tools.ietf.org/html/rfc5504">RFC5504</a>][<a href="https://tools.ietf.org/html/rfc6857">RFC6857 Section 3.1.10</a>]</td>
        </tr>
        <tr>
            <td>Downgraded-In-Reply-To</td>
            <td></td>
            <td>mail</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc6857">RFC6857 Section 3.1.10</a>]</td>
        </tr>
        <tr>
            <td>Downgraded-Mail-From</td>
            <td></td>
            <td>mail</td>
            <td>obsoleted</td>
            <td>[<a href="https://tools.ietf.org/html/rfc5504">RFC5504</a>][<a href="https://tools.ietf.org/html/rfc6857">RFC6857 Section 3.1.10</a>]</td>
        </tr>
        <tr>
            <td>Downgraded-Message-Id</td>
            <td></td>
            <td>mail</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc6857">RFC6857 Section 3.1.10</a>]</td>
        </tr>
        <tr>
            <td>Downgraded-Original-Recipient</td>
            <td></td>
            <td>mail</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc6857">RFC6857 Section 3.1.10</a>]</td>
        </tr>
        <tr>
            <td>Downgraded-Rcpt-To</td>
            <td></td>
            <td>mail</td>
            <td>obsoleted</td>
            <td>[<a href="https://tools.ietf.org/html/rfc5504">RFC5504</a>][<a href="https://tools.ietf.org/html/rfc6857">RFC6857</a>]</td>
        </tr>
        <tr>
            <td>Downgraded-References</td>
            <td></td>
            <td>mail</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc6857">RFC6857 Section 3.1.10</a>]</td>
        </tr>
        <tr>
            <td>Downgraded-Reply-To</td>
            <td></td>
            <td>mail</td>
            <td>obsoleted</td>
            <td>[<a href="https://tools.ietf.org/html/rfc5504">RFC5504</a>][<a href="https://tools.ietf.org/html/rfc6857">RFC6857</a>]</td>
        </tr>
        <tr>
            <td>Downgraded-Resent-Bcc</td>
            <td></td>
            <td>mail</td>
            <td>obsoleted</td>
            <td>[<a href="https://tools.ietf.org/html/rfc5504">RFC5504</a>][<a href="https://tools.ietf.org/html/rfc6857">RFC6857</a>]</td>
        </tr>
        <tr>
            <td>Downgraded-Resent-Cc</td>
            <td></td>
            <td>mail</td>
            <td>obsoleted</td>
            <td>[<a href="https://tools.ietf.org/html/rfc5504">RFC5504</a>][<a href="https://tools.ietf.org/html/rfc6857">RFC6857</a>]</td>
        </tr>
        <tr>
            <td>Downgraded-Resent-From</td>
            <td></td>
            <td>mail</td>
            <td>obsoleted</td>
            <td>[<a href="https://tools.ietf.org/html/rfc5504">RFC5504</a>][<a href="https://tools.ietf.org/html/rfc6857">RFC6857</a>]</td>
        </tr>
        <tr>
            <td>Downgraded-Resent-Reply-To</td>
            <td></td>
            <td>mail</td>
            <td>obsoleted</td>
            <td>[<a href="https://tools.ietf.org/html/rfc5504">RFC5504</a>][<a href="https://tools.ietf.org/html/rfc6857">RFC6857</a>]</td>
        </tr>
        <tr>
            <td>Downgraded-Resent-Sender</td>
            <td></td>
            <td>mail</td>
            <td>obsoleted</td>
            <td>[<a href="https://tools.ietf.org/html/rfc5504">RFC5504</a>][<a href="https://tools.ietf.org/html/rfc6857">RFC6857</a>]</td>
        </tr>
        <tr>
            <td>Downgraded-Resent-To</td>
            <td></td>
            <td>mail</td>
            <td>obsoleted</td>
            <td>[<a href="https://tools.ietf.org/html/rfc5504">RFC5504</a>][<a href="https://tools.ietf.org/html/rfc6857">RFC6857</a>]</td>
        </tr>
        <tr>
            <td>Downgraded-Return-Path</td>
            <td></td>
            <td>mail</td>
            <td>obsoleted</td>
            <td>[<a href="https://tools.ietf.org/html/rfc5504">RFC5504</a>][<a href="https://tools.ietf.org/html/rfc6857">RFC6857</a>]</td>
        </tr>
        <tr>
            <td>Downgraded-Sender</td>
            <td></td>
            <td>mail</td>
            <td>obsoleted</td>
            <td>[<a href="https://tools.ietf.org/html/rfc5504">RFC5504</a>][<a href="https://tools.ietf.org/html/rfc6857">RFC6857</a>]</td>
        </tr>
        <tr>
            <td>Downgraded-To</td>
            <td></td>
            <td>mail</td>
            <td>obsoleted</td>
            <td>[<a href="https://tools.ietf.org/html/rfc5504">RFC5504</a>][<a href="https://tools.ietf.org/html/rfc6857">RFC6857</a>]</td>
        </tr>
        <tr>
            <td>Early-Data</td>
            <td></td>
            <td>http</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/draft-ietf-httpbis-replay-04">RFC-ietf-httpbis-replay-04</a>]</td>
        </tr>
        <tr>
            <td>Encoding</td>
            <td></td>
            <td>mail</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4021">RFC4021</a>]</td>
        </tr>
        <tr>
            <td>Encrypted</td>
            <td></td>
            <td>mail</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4021">RFC4021</a>]</td>
        </tr>
        <tr>
            <td>ETag</td>
            <td></td>
            <td>http</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc7232">RFC7232, Section 2.3</a>]</td>
        </tr>
        <tr>
            <td>Expect</td>
            <td></td>
            <td>http</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc7231">RFC7231, Section 5.1.1</a>]</td>
        </tr>
        <tr>
            <td>Expires</td>
            <td></td>
            <td>http</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc7234">RFC7234, Section 5.3</a>]</td>
        </tr>
        <tr>
            <td>Expires</td>
            <td></td>
            <td>mail</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4021">RFC4021</a>]</td>
        </tr>
        <tr>
            <td>Expires</td>
            <td></td>
            <td>netnews</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc5536">RFC5536</a>]</td>
        </tr>
        <tr>
            <td>Expiry-Date</td>
            <td></td>
            <td>mail</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4021">RFC4021</a>]</td>
        </tr>
        <tr>
            <td>Ext</td>
            <td></td>
            <td>http</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4229">RFC4229</a>]</td>
        </tr>
        <tr>
            <td>Followup-To</td>
            <td></td>
            <td>netnews</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc5536">RFC5536</a>]</td>
        </tr>
        <tr>
            <td>Forwarded</td>
            <td></td>
            <td>http</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc7239">RFC7239</a>]</td>
        </tr>
        <tr>
            <td>From</td>
            <td></td>
            <td>http</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc7231">RFC7231, Section 5.5.1</a>]</td>
        </tr>
        <tr>
            <td>From</td>
            <td></td>
            <td>mail</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc5322">RFC5322</a>][<a href="https://tools.ietf.org/html/rfc6854">RFC6854</a>]</td>
        </tr>
        <tr>
            <td>From</td>
            <td></td>
            <td>netnews</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc5536">RFC5536</a>][<a href="https://tools.ietf.org/html/rfc5322">RFC5322</a>]</td>
        </tr>
        <tr>
            <td>Generate-Delivery-Report</td>
            <td></td>
            <td>mail</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4021">RFC4021</a>]</td>
        </tr>
        <tr>
            <td>GetProfile</td>
            <td></td>
            <td>http</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4229">RFC4229</a>]</td>
        </tr>
        <tr>
            <td>Hobareg</td>
            <td></td>
            <td>http</td>
            <td>experimental</td>
            <td>[<a href="https://tools.ietf.org/html/rfc7486">RFC7486, Section 6.1.1</a>]</td>
        </tr>
        <tr>
            <td>Host</td>
            <td></td>
            <td>http</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc7230">RFC7230, Section 5.4</a>]</td>
        </tr>
        <tr>
            <td>HTTP2-Settings</td>
            <td></td>
            <td>http</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc7540">RFC7540, Section 3.2.1</a>]</td>
        </tr>
        <tr>
            <td>IM</td>
            <td></td>
            <td>http</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4229">RFC4229</a>]</td>
        </tr>
        <tr>
            <td>If</td>
            <td></td>
            <td>http</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc4918">RFC4918</a>]</td>
        </tr>
        <tr>
            <td>If-Match</td>
            <td></td>
            <td>http</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc7232">RFC7232, Section 3.1</a>]</td>
        </tr>
        <tr>
            <td>If-Modified-Since</td>
            <td></td>
            <td>http</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc7232">RFC7232, Section 3.3</a>]</td>
        </tr>
        <tr>
            <td>If-None-Match</td>
            <td></td>
            <td>http</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc7232">RFC7232, Section 3.2</a>]</td>
        </tr>
        <tr>
            <td>If-Range</td>
            <td></td>
            <td>http</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc7233">RFC7233, Section 3.2</a>]</td>
        </tr>
        <tr>
            <td>If-Schedule-Tag-Match</td>
            <td></td>
            <td>http</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc6638">RFC6638</a>]</td>
        </tr>
        <tr>
            <td>If-Unmodified-Since</td>
            <td></td>
            <td>http</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc7232">RFC7232, Section 3.4</a>]</td>
        </tr>
        <tr>
            <td>Importance</td>
            <td></td>
            <td>mail</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4021">RFC4021</a>]</td>
        </tr>
        <tr>
            <td>In-Reply-To</td>
            <td></td>
            <td>mail</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc5322">RFC5322</a>]</td>
        </tr>
        <tr>
            <td>Include-Referred-Token-Binding-ID</td>
            <td></td>
            <td>http</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/draft-ietf-tokbind-https-18">RFC-ietf-tokbind-https-18</a>]</td>
        </tr>
        <tr>
            <td>Incomplete-Copy</td>
            <td></td>
            <td>mail</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4021">RFC4021</a>]</td>
        </tr>
        <tr>
            <td>Injection-Date</td>
            <td></td>
            <td>netnews</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc5536">RFC5536</a>]</td>
        </tr>
        <tr>
            <td>Injection-Info</td>
            <td></td>
            <td>netnews</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc5536">RFC5536</a>]</td>
        </tr>
        <tr>
            <td>Keep-Alive</td>
            <td></td>
            <td>http</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4229">RFC4229</a>]</td>
        </tr>
        <tr>
            <td>Keywords</td>
            <td></td>
            <td>mail</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc5322">RFC5322</a>]</td>
        </tr>
        <tr>
            <td>Keywords</td>
            <td></td>
            <td>netnews</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc5536">RFC5536</a>][<a href="https://tools.ietf.org/html/rfc5322">RFC5322</a>]</td>
        </tr>
        <tr>
            <td>Label</td>
            <td></td>
            <td>http</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4229">RFC4229</a>]</td>
        </tr>
        <tr>
            <td>Language</td>
            <td></td>
            <td>mail</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4021">RFC4021</a>]</td>
        </tr>
        <tr>
            <td>Last-Modified</td>
            <td></td>
            <td>http</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc7232">RFC7232, Section 2.2</a>]</td>
        </tr>
        <tr>
            <td>Latest-Delivery-Time</td>
            <td></td>
            <td>mail</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4021">RFC4021</a>]</td>
        </tr>
        <tr>
            <td>Lines</td>
            <td></td>
            <td>netnews</td>
            <td>deprecated</td>
            <td>[<a href="https://tools.ietf.org/html/rfc5536">RFC5536</a>][<a href="https://tools.ietf.org/html/rfc3977">RFC3977</a>]</td>
        </tr>
        <tr>
            <td>Link</td>
            <td></td>
            <td>http</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc8288">RFC8288</a>]</td>
        </tr>
        <tr>
            <td>List-Archive</td>
            <td></td>
            <td>mail</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4021">RFC4021</a>]</td>
        </tr>
        <tr>
            <td>List-Help</td>
            <td></td>
            <td>mail</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4021">RFC4021</a>]</td>
        </tr>
        <tr>
            <td>List-ID</td>
            <td></td>
            <td>mail</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4021">RFC4021</a>]</td>
        </tr>
        <tr>
            <td>List-Owner</td>
            <td></td>
            <td>mail</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4021">RFC4021</a>]</td>
        </tr>
        <tr>
            <td>List-Post</td>
            <td></td>
            <td>mail</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4021">RFC4021</a>]</td>
        </tr>
        <tr>
            <td>List-Subscribe</td>
            <td></td>
            <td>mail</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4021">RFC4021</a>]</td>
        </tr>
        <tr>
            <td>List-Unsubscribe</td>
            <td>
            <a href="perm/list-unsubscribe">perm/list-unsubscribe</a>
            </td>
            <td>mail</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4021">RFC4021</a>]</td>
        </tr>
        <tr>
            <td>List-Unsubscribe-Post</td>
            <td></td>
            <td>mail</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc8058">RFC8058</a>]</td>
        </tr>
        <tr>
            <td>Location</td>
            <td></td>
            <td>http</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc7231">RFC7231, Section 7.1.2</a>]</td>
        </tr>
        <tr>
            <td>Lock-Token</td>
            <td></td>
            <td>http</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc4918">RFC4918</a>]</td>
        </tr>
        <tr>
            <td>Man</td>
            <td></td>
            <td>http</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4229">RFC4229</a>]</td>
        </tr>
        <tr>
            <td>Max-Forwards</td>
            <td></td>
            <td>http</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc7231">RFC7231, Section 5.1.2</a>]</td>
        </tr>
        <tr>
            <td>Memento-Datetime</td>
            <td></td>
            <td>http</td>
            <td>informational</td>
            <td>[<a href="https://tools.ietf.org/html/rfc7089">RFC7089</a>]</td>
        </tr>
        <tr>
            <td>Message-Context</td>
            <td></td>
            <td>mail</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4021">RFC4021</a>]</td>
        </tr>
        <tr>
            <td>Message-ID</td>
            <td></td>
            <td>mail</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc5322">RFC5322</a>]</td>
        </tr>
        <tr>
            <td>Message-ID</td>
            <td></td>
            <td>netnews</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc5536">RFC5536</a>][<a href="https://tools.ietf.org/html/rfc5322">RFC5322</a>]</td>
        </tr>
        <tr>
            <td>Message-Type</td>
            <td></td>
            <td>mail</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4021">RFC4021</a>]</td>
        </tr>
        <tr>
            <td>Meter</td>
            <td></td>
            <td>http</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4229">RFC4229</a>]</td>
        </tr>
        <tr>
            <td>MIME-Version</td>
            <td></td>
            <td>http</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc7231">RFC7231, Appendix A.1</a>]</td>
        </tr>
        <tr>
            <td>MIME-Version</td>
            <td></td>
            <td>MIME</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4021">RFC4021</a>]</td>
        </tr>
        <tr>
            <td>MMHS-Exempted-Address</td>
            <td></td>
            <td>mail</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc6477">RFC6477</a>][<a href="http://jcs.dtic.mil/j6/cceb/acps/acp123/ACP123B.pdf">ACP123 Appendix A1.1 and Appendix B.105</a>]</td>
        </tr>
        <tr>
            <td>MMHS-Extended-Authorisation-Info</td>
            <td></td>
            <td>mail</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc6477">RFC6477</a>][<a href="http://jcs.dtic.mil/j6/cceb/acps/acp123/ACP123B.pdf">ACP123 Appendix A1.2 and Appendix B.106</a>]</td>
        </tr>
        <tr>
            <td>MMHS-Subject-Indicator-Codes</td>
            <td></td>
            <td>mail</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc6477">RFC6477</a>][<a href="http://jcs.dtic.mil/j6/cceb/acps/acp123/ACP123B.pdf">ACP123 Appendix A1.3 and Appendix B.107</a>]</td>
        </tr>
        <tr>
            <td>MMHS-Handling-Instructions</td>
            <td></td>
            <td>mail</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc6477">RFC6477</a>][<a href="http://jcs.dtic.mil/j6/cceb/acps/acp123/ACP123B.pdf">ACP123 Appendix A1.4 and Appendix B.108</a>]</td>
        </tr>
        <tr>
            <td>MMHS-Message-Instructions</td>
            <td></td>
            <td>mail</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc6477">RFC6477</a>][<a href="http://jcs.dtic.mil/j6/cceb/acps/acp123/ACP123B.pdf">ACP123 Appendix A1.5 and Appendix B.109</a>]</td>
        </tr>
        <tr>
            <td>MMHS-Codress-Message-Indicator</td>
            <td></td>
            <td>mail</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc6477">RFC6477</a>][<a href="http://jcs.dtic.mil/j6/cceb/acps/acp123/ACP123B.pdf">ACP123 Appendix A1.6 and Appendix B.110</a>]</td>
        </tr>
        <tr>
            <td>MMHS-Originator-Reference</td>
            <td></td>
            <td>mail</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc6477">RFC6477</a>][<a href="http://jcs.dtic.mil/j6/cceb/acps/acp123/ACP123B.pdf">ACP123 Appendix A1.7 and Appendix B.111</a>]</td>
        </tr>
        <tr>
            <td>MMHS-Primary-Precedence</td>
            <td></td>
            <td>mail</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc6477">RFC6477</a>][<a href="http://jcs.dtic.mil/j6/cceb/acps/acp123/ACP123B.pdf">ACP123 Appendix A1.8 and Appendix B.101</a>]</td>
        </tr>
        <tr>
            <td>MMHS-Copy-Precedence</td>
            <td></td>
            <td>mail</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc6477">RFC6477</a>][<a href="http://jcs.dtic.mil/j6/cceb/acps/acp123/ACP123B.pdf">ACP123 Appendix A1.9 and Appendix B.102</a>]</td>
        </tr>
        <tr>
            <td>MMHS-Message-Type</td>
            <td></td>
            <td>mail</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc6477">RFC6477</a>][<a href="http://jcs.dtic.mil/j6/cceb/acps/acp123/ACP123B.pdf">ACP123 Appendix A1.10 and Appendix B.103</a>]</td>
        </tr>
        <tr>
            <td>MMHS-Other-Recipients-Indicator-To</td>
            <td></td>
            <td>mail</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc6477">RFC6477</a>][<a href="http://jcs.dtic.mil/j6/cceb/acps/acp123/ACP123B.pdf">ACP123 Appendix A1.12 and Appendix B.113</a>]</td>
        </tr>
        <tr>
            <td>MMHS-Other-Recipients-Indicator-CC</td>
            <td></td>
            <td>mail</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc6477">RFC6477</a>][<a href="http://jcs.dtic.mil/j6/cceb/acps/acp123/ACP123B.pdf">ACP123 Appendix A1.12 and Appendix B.113</a>]</td>
        </tr>
        <tr>
            <td>MMHS-Acp127-Message-Identifier</td>
            <td></td>
            <td>mail</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc6477">RFC6477</a>][<a href="http://jcs.dtic.mil/j6/cceb/acps/acp123/ACP123B.pdf">ACP123 Appendix A1.14 and Appendix B.116</a>]</td>
        </tr>
        <tr>
            <td>MMHS-Originator-PLAD</td>
            <td></td>
            <td>mail</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc6477">RFC6477</a>][<a href="http://jcs.dtic.mil/j6/cceb/acps/acp123/ACP123B.pdf">ACP123 Appendix A1.15 and Appendix B.117</a>]</td>
        </tr>
        <tr>
            <td>MT-Priority</td>
            <td></td>
            <td>mail</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc6758">RFC6758</a>]</td>
        </tr>
        <tr>
            <td>Negotiate</td>
            <td></td>
            <td>http</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4229">RFC4229</a>]</td>
        </tr>
        <tr>
            <td>Newsgroups</td>
            <td></td>
            <td>netnews</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc5536">RFC5536</a>]</td>
        </tr>
        <tr>
            <td>NNTP-Posting-Date</td>
            <td></td>
            <td>netnews</td>
            <td>obsoleted</td>
            <td>[<a href="https://tools.ietf.org/html/rfc5536">RFC5536</a>]</td>
        </tr>
        <tr>
            <td>NNTP-Posting-Host</td>
            <td></td>
            <td>netnews</td>
            <td>obsoleted</td>
            <td>[<a href="https://tools.ietf.org/html/rfc2980">RFC2980</a>][<a href="https://tools.ietf.org/html/rfc5536">RFC5536</a>]</td>
        </tr>
        <tr>
            <td>Obsoletes</td>
            <td></td>
            <td>mail</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4021">RFC4021</a>]</td>
        </tr>
        <tr>
            <td>Opt</td>
            <td></td>
            <td>http</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4229">RFC4229</a>]</td>
        </tr>
        <tr>
            <td>Optional-WWW-Authenticate</td>
            <td></td>
            <td>http</td>
            <td>experimental</td>
            <td>[<a href="https://tools.ietf.org/html/rfc8053">RFC8053, Section 3</a>]</td>
        </tr>
        <tr>
            <td>Ordering-Type</td>
            <td></td>
            <td>http</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc4229">RFC4229</a>]</td>
        </tr>
        <tr>
            <td>Organization</td>
            <td></td>
            <td>mail</td>
            <td>informational</td>
            <td>[<a href="https://tools.ietf.org/html/rfc7681">RFC7681</a>]</td>
        </tr>
        <tr>
            <td>Organization</td>
            <td></td>
            <td>netnews</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc5536">RFC5536</a>]</td>
        </tr>
        <tr>
            <td>Origin</td>
            <td></td>
            <td>http</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc6454">RFC6454</a>]</td>
        </tr>
        <tr>
            <td>Original-Encoded-Information-Types</td>
            <td></td>
            <td>mail</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4021">RFC4021</a>]</td>
        </tr>
        <tr>
            <td>Original-From</td>
            <td></td>
            <td>mail</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc5703">RFC5703</a>]</td>
        </tr>
        <tr>
            <td>Original-Message-ID</td>
            <td></td>
            <td>mail</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4021">RFC4021</a>]</td>
        </tr>
        <tr>
            <td>Original-Recipient</td>
            <td>
            <a href="perm/original-recipient">perm/original-recipient</a>
            </td>
            <td>mail</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc3798">RFC3798</a>][<a href="https://tools.ietf.org/html/rfc5337">RFC5337</a>]</td>
        </tr>
        <tr>
            <td>Original-Sender</td>
            <td></td>
            <td>netnews</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc5537">RFC5537</a>]</td>
        </tr>
        <tr>
            <td>Originator-Return-Address</td>
            <td></td>
            <td>mail</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4021">RFC4021</a>]</td>
        </tr>
        <tr>
            <td>Original-Subject</td>
            <td></td>
            <td>mail</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc5703">RFC5703</a>]</td>
        </tr>
        <tr>
            <td>Overwrite</td>
            <td></td>
            <td>http</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc4918">RFC4918</a>]</td>
        </tr>
        <tr>
            <td>P3P</td>
            <td></td>
            <td>http</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4229">RFC4229</a>]</td>
        </tr>
        <tr>
            <td>Path</td>
            <td></td>
            <td>netnews</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc5536">RFC5536</a>]</td>
        </tr>
        <tr>
            <td>PEP</td>
            <td></td>
            <td>http</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4229">RFC4229</a>]</td>
        </tr>
        <tr>
            <td>PICS-Label</td>
            <td></td>
            <td>http</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4229">RFC4229</a>]</td>
        </tr>
        <tr>
            <td>PICS-Label</td>
            <td></td>
            <td>mail</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4021">RFC4021</a>]</td>
        </tr>
        <tr>
            <td>Pep-Info</td>
            <td></td>
            <td>http</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4229">RFC4229</a>]</td>
        </tr>
        <tr>
            <td>Position</td>
            <td></td>
            <td>http</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc4229">RFC4229</a>]</td>
        </tr>
        <tr>
            <td>Posting-Version</td>
            <td></td>
            <td>netnews</td>
            <td>obsoleted</td>
            <td>[<a href="https://tools.ietf.org/html/rfc0850">RFC0850</a>][<a href="https://tools.ietf.org/html/rfc5536">RFC5536</a>]</td>
        </tr>
        <tr>
            <td>Pragma</td>
            <td></td>
            <td>http</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc7234">RFC7234, Section 5.4</a>]</td>
        </tr>
        <tr>
            <td>Prefer</td>
            <td></td>
            <td>http</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc7240">RFC7240</a>]</td>
        </tr>
        <tr>
            <td>Preference-Applied</td>
            <td></td>
            <td>http</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc7240">RFC7240</a>]</td>
        </tr>
        <tr>
            <td>Prevent-NonDelivery-Report</td>
            <td></td>
            <td>mail</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4021">RFC4021</a>]</td>
        </tr>
        <tr>
            <td>Priority</td>
            <td></td>
            <td>mail</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4021">RFC4021</a>]</td>
        </tr>
        <tr>
            <td>ProfileObject</td>
            <td></td>
            <td>http</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4229">RFC4229</a>]</td>
        </tr>
        <tr>
            <td>Protocol</td>
            <td></td>
            <td>http</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4229">RFC4229</a>]</td>
        </tr>
        <tr>
            <td>Protocol-Info</td>
            <td></td>
            <td>http</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4229">RFC4229</a>]</td>
        </tr>
        <tr>
            <td>Protocol-Query</td>
            <td></td>
            <td>http</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4229">RFC4229</a>]</td>
        </tr>
        <tr>
            <td>Protocol-Request</td>
            <td></td>
            <td>http</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4229">RFC4229</a>]</td>
        </tr>
        <tr>
            <td>Proxy-Authenticate</td>
            <td></td>
            <td>http</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc7235">RFC7235, Section 4.3</a>]</td>
        </tr>
        <tr>
            <td>Proxy-Authentication-Info</td>
            <td></td>
            <td>http</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc7615">RFC7615, Section 4</a>]</td>
        </tr>
        <tr>
            <td>Proxy-Authorization</td>
            <td></td>
            <td>http</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc7235">RFC7235, Section 4.4</a>]</td>
        </tr>
        <tr>
            <td>Proxy-Features</td>
            <td></td>
            <td>http</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4229">RFC4229</a>]</td>
        </tr>
        <tr>
            <td>Proxy-Instruction</td>
            <td></td>
            <td>http</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4229">RFC4229</a>]</td>
        </tr>
        <tr>
            <td>Public</td>
            <td></td>
            <td>http</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4229">RFC4229</a>]</td>
        </tr>
        <tr>
            <td>Public-Key-Pins</td>
            <td></td>
            <td>http</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc7469">RFC7469</a>]</td>
        </tr>
        <tr>
            <td>Public-Key-Pins-Report-Only</td>
            <td></td>
            <td>http</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc7469">RFC7469</a>]</td>
        </tr>
        <tr>
            <td>Range</td>
            <td></td>
            <td>http</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc7233">RFC7233, Section 3.1</a>]</td>
        </tr>
        <tr>
            <td>Received</td>
            <td></td>
            <td>mail</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc5322">RFC5322</a>][<a href="https://tools.ietf.org/html/rfc5321">RFC5321</a>]</td>
        </tr>
        <tr>
            <td>Received-SPF</td>
            <td></td>
            <td>mail</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc7208">RFC7208</a>]</td>
        </tr>
        <tr>
            <td>Redirect-Ref</td>
            <td></td>
            <td>http</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4437">RFC4437</a>]</td>
        </tr>
        <tr>
            <td>References</td>
            <td></td>
            <td>mail</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc5322">RFC5322</a>]</td>
        </tr>
        <tr>
            <td>References</td>
            <td></td>
            <td>netnews</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc5536">RFC5536</a>][<a href="https://tools.ietf.org/html/rfc5322">RFC5322</a>]</td>
        </tr>
        <tr>
            <td>Referer</td>
            <td></td>
            <td>http</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc7231">RFC7231, Section 5.5.2</a>]</td>
        </tr>
        <tr>
            <td>Relay-Version</td>
            <td></td>
            <td>netnews</td>
            <td>obsoleted</td>
            <td>[<a href="https://tools.ietf.org/html/rfc0850">RFC0850</a>][<a href="https://tools.ietf.org/html/rfc5536">RFC5536</a>]</td>
        </tr>
        <tr>
            <td>Reply-By</td>
            <td></td>
            <td>mail</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4021">RFC4021</a>]</td>
        </tr>
        <tr>
            <td>Reply-To</td>
            <td></td>
            <td>mail</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc5322">RFC5322</a>]</td>
        </tr>
        <tr>
            <td>Reply-To</td>
            <td></td>
            <td>netnews</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc5536">RFC5536</a>][<a href="https://tools.ietf.org/html/rfc5322">RFC5322</a>]</td>
        </tr>
        <tr>
            <td>Require-Recipient-Valid-Since</td>
            <td></td>
            <td>mail</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc7293">RFC7293</a>]</td>
        </tr>
        <tr>
            <td>Resent-Bcc</td>
            <td></td>
            <td>mail</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc5322">RFC5322</a>]</td>
        </tr>
        <tr>
            <td>Resent-Cc</td>
            <td></td>
            <td>mail</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc5322">RFC5322</a>]</td>
        </tr>
        <tr>
            <td>Resent-Date</td>
            <td></td>
            <td>mail</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc5322">RFC5322</a>]</td>
        </tr>
        <tr>
            <td>Resent-From</td>
            <td></td>
            <td>mail</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc5322">RFC5322</a>][<a href="https://tools.ietf.org/html/rfc6854">RFC6854</a>]</td>
        </tr>
        <tr>
            <td>Resent-Message-ID</td>
            <td></td>
            <td>mail</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc5322">RFC5322</a>]</td>
        </tr>
        <tr>
            <td>Resent-Reply-To</td>
            <td></td>
            <td>mail</td>
            <td>obsoleted</td>
            <td>[<a href="https://tools.ietf.org/html/rfc5322">RFC5322</a>]</td>
        </tr>
        <tr>
            <td>Resent-Sender</td>
            <td></td>
            <td>mail</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc5322">RFC5322</a>][<a href="https://tools.ietf.org/html/rfc6854">RFC6854</a>]</td>
        </tr>
        <tr>
            <td>Resent-To</td>
            <td></td>
            <td>mail</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc5322">RFC5322</a>]</td>
        </tr>
        <tr>
            <td>Retry-After</td>
            <td></td>
            <td>http</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc7231">RFC7231, Section 7.1.3</a>]</td>
        </tr>
        <tr>
            <td>Return-Path</td>
            <td></td>
            <td>mail</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc5322">RFC5322</a>]</td>
        </tr>
        <tr>
            <td>Safe</td>
            <td></td>
            <td>http</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4229">RFC4229</a>]</td>
        </tr>
        <tr>
            <td>Schedule-Reply</td>
            <td></td>
            <td>http</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc6638">RFC6638</a>]</td>
        </tr>
        <tr>
            <td>Schedule-Tag</td>
            <td></td>
            <td>http</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc6638">RFC6638</a>]</td>
        </tr>
        <tr>
            <td>Sec-Token-Binding</td>
            <td></td>
            <td>http</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/draft-ietf-tokbind-https-18">RFC-ietf-tokbind-https-18</a>]</td>
        </tr>
        <tr>
            <td>Sec-WebSocket-Accept</td>
            <td></td>
            <td>http</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc6455">RFC6455</a>]</td>
        </tr>
        <tr>
            <td>Sec-WebSocket-Extensions</td>
            <td></td>
            <td>http</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc6455">RFC6455</a>]</td>
        </tr>
        <tr>
            <td>Sec-WebSocket-Key</td>
            <td></td>
            <td>http</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc6455">RFC6455</a>]</td>
        </tr>
        <tr>
            <td>Sec-WebSocket-Protocol</td>
            <td></td>
            <td>http</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc6455">RFC6455</a>]</td>
        </tr>
        <tr>
            <td>Sec-WebSocket-Version</td>
            <td></td>
            <td>http</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc6455">RFC6455</a>]</td>
        </tr>
        <tr>
            <td>Security-Scheme</td>
            <td></td>
            <td>http</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4229">RFC4229</a>]</td>
        </tr>
        <tr>
            <td>See-Also</td>
            <td></td>
            <td>netnews</td>
            <td>obsoleted</td>
            <td>[<a href="https://tools.ietf.org/html/rfc1849">RFC1849</a>][<a href="https://tools.ietf.org/html/rfc5536">RFC5536</a>]</td>
        </tr>
        <tr>
            <td>Sender</td>
            <td></td>
            <td>mail</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc5322">RFC5322</a>][<a href="https://tools.ietf.org/html/rfc6854">RFC6854</a>]</td>
        </tr>
        <tr>
            <td>Sender</td>
            <td></td>
            <td>netnews</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc5536">RFC5536</a>][<a href="https://tools.ietf.org/html/rfc5322">RFC5322</a>]</td>
        </tr>
        <tr>
            <td>Sensitivity</td>
            <td></td>
            <td>mail</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4021">RFC4021</a>]</td>
        </tr>
        <tr>
            <td>Server</td>
            <td></td>
            <td>http</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc7231">RFC7231, Section 7.4.2</a>]</td>
        </tr>
        <tr>
            <td>Set-Cookie</td>
            <td></td>
            <td>http</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc6265">RFC6265</a>]</td>
        </tr>
        <tr>
            <td>Set-Cookie2</td>
            <td></td>
            <td>http</td>
            <td>obsoleted</td>
            <td>[<a href="https://tools.ietf.org/html/rfc2965">RFC2965</a>][<a href="https://tools.ietf.org/html/rfc6265">RFC6265</a>]</td>
        </tr>
        <tr>
            <td>SetProfile</td>
            <td></td>
            <td>http</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4229">RFC4229</a>]</td>
        </tr>
        <tr>
            <td>SLUG</td>
            <td></td>
            <td>http</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc5023">RFC5023</a>]</td>
        </tr>
        <tr>
            <td>SoapAction</td>
            <td></td>
            <td>http</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4229">RFC4229</a>]</td>
        </tr>
        <tr>
            <td>Solicitation</td>
            <td></td>
            <td>mail</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc3865">RFC3865</a>]</td>
        </tr>
        <tr>
            <td>Status-URI</td>
            <td></td>
            <td>http</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4229">RFC4229</a>]</td>
        </tr>
        <tr>
            <td>Strict-Transport-Security</td>
            <td></td>
            <td>http</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc6797">RFC6797</a>]</td>
        </tr>
        <tr>
            <td>Subject</td>
            <td></td>
            <td>mail</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc5322">RFC5322</a>]</td>
        </tr>
        <tr>
            <td>Subject</td>
            <td></td>
            <td>netnews</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc5536">RFC5536</a>][<a href="https://tools.ietf.org/html/rfc5322">RFC5322</a>]</td>
        </tr>
        <tr>
            <td>Summary</td>
            <td></td>
            <td>netnews</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc5536">RFC5536</a>]</td>
        </tr>
        <tr>
            <td>Supersedes</td>
            <td></td>
            <td>mail</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4021">RFC4021</a>]</td>
        </tr>
        <tr>
            <td>Supersedes</td>
            <td></td>
            <td>netnews</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc5536">RFC5536</a>][<a href="https://tools.ietf.org/html/rfc2156">RFC2156</a>]</td>
        </tr>
        <tr>
            <td>Surrogate-Capability</td>
            <td></td>
            <td>http</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4229">RFC4229</a>]</td>
        </tr>
        <tr>
            <td>Surrogate-Control</td>
            <td></td>
            <td>http</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4229">RFC4229</a>]</td>
        </tr>
        <tr>
            <td>TCN</td>
            <td></td>
            <td>http</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4229">RFC4229</a>]</td>
        </tr>
        <tr>
            <td>TE</td>
            <td></td>
            <td>http</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc7230">RFC7230, Section 4.3</a>]</td>
        </tr>
        <tr>
            <td>Timeout</td>
            <td></td>
            <td>http</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc4918">RFC4918</a>]</td>
        </tr>
        <tr>
            <td>TLS-Report-Domain</td>
            <td></td>
            <td>mail</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/draft-ietf-uta-smtp-tlsrpt-23">RFC-ietf-uta-smtp-tlsrpt-23</a>]</td>
        </tr>
        <tr>
            <td>TLS-Report-Submitter</td>
            <td></td>
            <td>mail</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/draft-ietf-uta-smtp-tlsrpt-23">RFC-ietf-uta-smtp-tlsrpt-23</a>]</td>
        </tr>
        <tr>
            <td>To</td>
            <td></td>
            <td>mail</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc5322">RFC5322</a>]</td>
        </tr>
        <tr>
            <td>Topic</td>
            <td></td>
            <td>http</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc8030">RFC8030, Section 5.4</a>]</td>
        </tr>
        <tr>
            <td>Trailer</td>
            <td></td>
            <td>http</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc7230">RFC7230, Section 4.4</a>]</td>
        </tr>
        <tr>
            <td>Transfer-Encoding</td>
            <td></td>
            <td>http</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc7230">RFC7230, Section 3.3.1</a>]</td>
        </tr>
        <tr>
            <td>TTL</td>
            <td></td>
            <td>http</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc8030">RFC8030, Section 5.2</a>]</td>
        </tr>
        <tr>
            <td>Urgency</td>
            <td></td>
            <td>http</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc8030">RFC8030, Section 5.3</a>]</td>
        </tr>
        <tr>
            <td>URI</td>
            <td></td>
            <td>http</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4229">RFC4229</a>]</td>
        </tr>
        <tr>
            <td>Upgrade</td>
            <td></td>
            <td>http</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc7230">RFC7230, Section 6.7</a>]</td>
        </tr>
        <tr>
            <td>User-Agent</td>
            <td></td>
            <td>http</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc7231">RFC7231, Section 5.5.3</a>]</td>
        </tr>
        <tr>
            <td>User-Agent</td>
            <td></td>
            <td>netnews</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc5536">RFC5536</a>][<a href="https://tools.ietf.org/html/rfc2616">RFC2616</a>]</td>
        </tr>
        <tr>
            <td>Variant-Vary</td>
            <td></td>
            <td>http</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4229">RFC4229</a>]</td>
        </tr>
        <tr>
            <td>Vary</td>
            <td></td>
            <td>http</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc7231">RFC7231, Section 7.1.4</a>]</td>
        </tr>
        <tr>
            <td>VBR-Info</td>
            <td></td>
            <td>mail</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc5518">RFC5518</a>]</td>
        </tr>
        <tr>
            <td>Via</td>
            <td></td>
            <td>http</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc7230">RFC7230, Section 5.7.1</a>]</td>
        </tr>
        <tr>
            <td>WWW-Authenticate</td>
            <td></td>
            <td>http</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc7235">RFC7235, Section 4.1</a>]</td>
        </tr>
        <tr>
            <td>Want-Digest</td>
            <td></td>
            <td>http</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4229">RFC4229</a>]</td>
        </tr>
        <tr>
            <td>Warning</td>
            <td></td>
            <td>http</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc7234">RFC7234, Section 5.5</a>]</td>
        </tr>
        <tr>
            <td>X400-Content-Identifier</td>
            <td></td>
            <td>mail</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4021">RFC4021</a>]</td>
        </tr>
        <tr>
            <td>X400-Content-Return</td>
            <td></td>
            <td>mail</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4021">RFC4021</a>]</td>
        </tr>
        <tr>
            <td>X400-Content-Type</td>
            <td></td>
            <td>mail</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4021">RFC4021</a>]</td>
        </tr>
        <tr>
            <td>X400-MTS-Identifier</td>
            <td></td>
            <td>mail</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4021">RFC4021</a>]</td>
        </tr>
        <tr>
            <td>X400-Originator</td>
            <td></td>
            <td>mail</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4021">RFC4021</a>]</td>
        </tr>
        <tr>
            <td>X400-Received</td>
            <td></td>
            <td>mail</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4021">RFC4021</a>]</td>
        </tr>
        <tr>
            <td>X400-Recipients</td>
            <td></td>
            <td>mail</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4021">RFC4021</a>]</td>
        </tr>
        <tr>
            <td>X400-Trace</td>
            <td></td>
            <td>mail</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4021">RFC4021</a>]</td>
        </tr>
        <tr>
            <td>X-Content-Type-Options</td>
            <td></td>
            <td>http</td>
            <td>standard</td>
            <td>[<a href="https://fetch.spec.whatwg.org/#x-content-type-options-header">https://fetch.spec.whatwg.org/#x-content-type-options-header</a>]</td>
        </tr>
        <tr>
            <td>X-Frame-Options</td>
            <td></td>
            <td>http</td>
            <td>informational</td>
            <td>[<a href="https://tools.ietf.org/html/rfc7034">RFC7034</a>]</td>
        </tr>
        <tr>
            <td>Xref</td>
            <td></td>
            <td>netnews</td>
            <td>standard</td>
            <td>[<a href="https://tools.ietf.org/html/rfc5536">RFC5536</a>]</td>
        </tr>
    </tbody>
</table>


#### Provisional Message Header Field Names ####

<dl>
    <dt>Registration Procedure(s)</dt>
    <dd>
        <pre>Expert Review</pre>
    </dd>
    <dt>Expert(s)</dt>
    <dd>
        <pre>Graham Klyne</pre>
    </dd>
    <dt>Reference</dt>
    <dd>[<a href="https://tools.ietf.org/html/rfc3864">RFC3864</a>]</dd>
    <dt>Note</dt>
    <dd>
        <pre>Registration of a Provisional Message Header Field does not of itself imply any kind of endorsement by the IETF, IANA or any other body.</pre>
    </dd>
    <dt><br></dt>
    <dd></dd>
</dl>

<table id="table-prov-headers" class="sortable">
    <thead>
        <tr style="cursor: pointer;">
            <td>Header Field Name</td>
            <td>Template</td>
            <td>Protocol</td>
            <td>Status</td>
            <td>Reference</td>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>Access-Control</td>
            <td>
            <a href="prov/access-control">prov/access-control</a>
            </td>
            <td>http</td>
            <td>deprecated</td>
            <td>[<a href="http://www.w3.org/2006/appformats/">W3C Web Application Formats Working Group</a>]</td>
        </tr>
        <tr>
            <td>Access-Control-Allow-Credentials</td>
            <td>
            <a href="prov/access-control-allow-credentials">prov/access-control-allow-credentials</a>
            </td>
            <td>http</td>
            <td></td>
            <td>[<a href="http://www.w3.org/2006/appformats/">W3C Web Application Formats Working Group</a>]</td>
        </tr>
        <tr>
            <td>Access-Control-Allow-Headers</td>
            <td>
            <a href="prov/access-control-allow-headers">prov/access-control-allow-headers</a>
            </td>
            <td>http</td>
            <td></td>
            <td>[<a href="http://www.w3.org/2006/appformats/">W3C Web Application Formats Working Group</a>]</td>
        </tr>
        <tr>
            <td>Access-Control-Allow-Methods</td>
            <td>
            <a href="prov/access-control-allow-methods">prov/access-control-allow-methods</a>
            </td>
            <td>http</td>
            <td></td>
            <td>[<a href="http://www.w3.org/2006/appformats/">W3C Web Application Formats Working Group</a>]</td>
        </tr>
        <tr>
            <td>Access-Control-Allow-Origin</td>
            <td>
            <a href="prov/access-control-allow-origin">prov/access-control-allow-origin</a>
            </td>
            <td>http</td>
            <td></td>
            <td>[<a href="http://www.w3.org/2006/appformats/">W3C Web Application Formats Working Group</a>]</td>
        </tr>
        <tr>
            <td>Access-Control-Max-Age</td>
            <td>
            <a href="prov/access-control-max-age">prov/access-control-max-age</a>
            </td>
            <td>http</td>
            <td></td>
            <td>[<a href="http://www.w3.org/2006/appformats/">W3C Web Application Formats Working Group</a>]</td>
        </tr>
        <tr>
            <td>Access-Control-Request-Method</td>
            <td>
            <a href="prov/access-control-request-method">prov/access-control-request-method</a>
            </td>
            <td>http</td>
            <td></td>
            <td>[<a href="http://www.w3.org/2006/appformats/">W3C Web Application Formats Working Group</a>]</td>
        </tr>
        <tr>
            <td>Access-Control-Request-Headers</td>
            <td>
            <a href="prov/access-control-request-headers">prov/access-control-request-headers</a>
            </td>
            <td>http</td>
            <td></td>
            <td>[<a href="http://www.w3.org/2006/appformats/">W3C Web Application Formats Working Group</a>]</td>
        </tr>
        <tr>
            <td>Apparently-To</td>
            <td>
            <a href="prov/apparently-to">prov/apparently-to</a>
            </td>
            <td>mail</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc2076">RFC2076</a>]</td>
        </tr>
        <tr>
            <td>ARC-Authentication-Results</td>
            <td>
            <a href="prov/arc-authentication-results">prov/arc-authentication-results</a>
            </td>
            <td>mail</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/draft-ietf-dmarc-arc-protocol">draft-ietf-dmarc-arc-protocol</a>]</td>
        </tr>
        <tr>
            <td>ARC-Message-Signature</td>
            <td>
            <a href="prov/arc-message-signature">prov/arc-message-signature</a>
            </td>
            <td>mail</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/draft-ietf-dmarc-arc-protocol">draft-ietf-dmarc-arc-protocol</a>]</td>
        </tr>
        <tr>
            <td>ARC-Seal</td>
            <td>
            <a href="prov/arc-seal">prov/arc-seal</a>
            </td>
            <td>mail</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/draft-ietf-dmarc-arc-protocol">draft-ietf-dmarc-arc-protocol</a>]</td>
        </tr>
        <tr>
            <td>Compliance</td>
            <td></td>
            <td>http</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4229">RFC4229</a>]</td>
        </tr>
        <tr>
            <td>Content-Transfer-Encoding</td>
            <td></td>
            <td>http</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4229">RFC4229</a>]</td>
        </tr>
        <tr>
            <td>Cost</td>
            <td></td>
            <td>http</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4229">RFC4229</a>]</td>
        </tr>
        <tr>
            <td>EDIINT-Features</td>
            <td></td>
            <td>http</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc6017">RFC6017</a>]</td>
        </tr>
        <tr>
            <td>EDIINT-Features</td>
            <td></td>
            <td>mail</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc6017">RFC6017</a>]</td>
        </tr>
        <tr>
            <td>Eesst-Version</td>
            <td></td>
            <td>mail</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc7681">RFC7681</a>]</td>
        </tr>
        <tr>
            <td>Errors-To</td>
            <td>
            <a href="prov/errors-to">prov/errors-to</a>
            </td>
            <td>mail</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc2076">RFC2076</a>]</td>
        </tr>
        <tr>
            <td>Form-Sub</td>
            <td></td>
            <td>mail</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/draft-levine-mailbomb-header">draft-levine-mailbomb-header</a>]</td>
        </tr>
        <tr>
            <td>Jabber-ID</td>
            <td>
            <a href="prov/jabber-id">prov/jabber-id</a>
            </td>
            <td>mail</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc7259">RFC7259</a>]</td>
        </tr>
        <tr>
            <td>Jabber-ID</td>
            <td>
            <a href="prov/jabber-id">prov/jabber-id</a>
            </td>
            <td>netnews</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc7259">RFC7259</a>]</td>
        </tr>
        <tr>
            <td>Message-ID</td>
            <td></td>
            <td>http</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4229">RFC4229</a>]</td>
        </tr>
        <tr>
            <td>Method-Check</td>
            <td>
            <a href="prov/method-check">prov/method-check</a>
            </td>
            <td>http</td>
            <td>deprecated</td>
            <td>[<a href="http://www.w3.org/2006/appformats/">W3C Web Application Formats Working Group</a>]</td>
        </tr>
        <tr>
            <td>Method-Check-Expires</td>
            <td>
            <a href="prov/method-check-expires">prov/method-check-expires</a>
            </td>
            <td>http</td>
            <td>deprecated</td>
            <td>[<a href="http://www.w3.org/2006/appformats/">W3C Web Application Formats Working Group</a>]</td>
        </tr>
        <tr>
            <td>MMHS-Authorizing-Users</td>
            <td></td>
            <td>mail</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc7912">RFC7912</a>]</td>
        </tr>
        <tr>
            <td>Non-Compliance</td>
            <td></td>
            <td>http</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4229">RFC4229</a>]</td>
        </tr>
        <tr>
            <td>Optional</td>
            <td></td>
            <td>http</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4229">RFC4229</a>]</td>
        </tr>
        <tr>
            <td>Privicon</td>
            <td></td>
            <td>mail</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/draft-koenig-privicons">draft-koenig-privicons</a>]</td>
        </tr>
        <tr>
            <td>Referer-Root</td>
            <td>
            <a href="prov/referer-root">prov/referer-root</a>
            </td>
            <td>http</td>
            <td>deprecated</td>
            <td>[<a href="http://www.w3.org/2006/appformats/">W3C Web Application Formats Working Group</a>]</td>
        </tr>
        <tr>
            <td>Resolution-Hint</td>
            <td></td>
            <td>http</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4229">RFC4229</a>]</td>
        </tr>
        <tr>
            <td>Resolver-Location</td>
            <td></td>
            <td>http</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4229">RFC4229</a>]</td>
        </tr>
        <tr>
            <td>SIO-Label</td>
            <td></td>
            <td>mail</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc7444">RFC7444</a>]</td>
        </tr>
        <tr>
            <td>SIO-Label-History</td>
            <td></td>
            <td>mail</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc7444">RFC7444</a>]</td>
        </tr>
        <tr>
            <td>SubOK</td>
            <td></td>
            <td>http</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4229">RFC4229</a>]</td>
        </tr>
        <tr>
            <td>Subst</td>
            <td></td>
            <td>http</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4229">RFC4229</a>]</td>
        </tr>
        <tr>
            <td>Title</td>
            <td></td>
            <td>http</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4229">RFC4229</a>]</td>
        </tr>
        <tr>
            <td>UA-Color</td>
            <td></td>
            <td>http</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4229">RFC4229</a>]</td>
        </tr>
        <tr>
            <td>UA-Media</td>
            <td></td>
            <td>http</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4229">RFC4229</a>]</td>
        </tr>
        <tr>
            <td>UA-Pixels</td>
            <td></td>
            <td>http</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4229">RFC4229</a>]</td>
        </tr>
        <tr>
            <td>UA-Resolution</td>
            <td></td>
            <td>http</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4229">RFC4229</a>]</td>
        </tr>
        <tr>
            <td>UA-Windowpixels</td>
            <td></td>
            <td>http</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4229">RFC4229</a>]</td>
        </tr>
        <tr>
            <td>Version</td>
            <td></td>
            <td>http</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc4229">RFC4229</a>]</td>
        </tr>
        <tr>
            <td>X-Archived-At</td>
            <td>
            <a href="prov/x-archived-at">prov/x-archived-at</a>
            </td>
            <td>mail</td>
            <td>deprecated</td>
            <td>[<a href="https://tools.ietf.org/html/rfc5064">RFC5064</a>]</td>
        </tr>
        <tr>
            <td>X-Archived-At</td>
            <td>
            <a href="prov/x-archived-at">prov/x-archived-at</a>
            </td>
            <td>netnews</td>
            <td>deprecated</td>
            <td>[<a href="https://tools.ietf.org/html/rfc5064">RFC5064</a>]</td>
        </tr>
        <tr>
            <td>X-Device-Accept</td>
            <td>
            <a href="prov/x-device-accept">prov/x-device-accept</a>
            </td>
            <td>http</td>
            <td></td>
            <td>[<a href="http://www.w3.org/2005/MWI/BPWG/">W3C Mobile Web Best Practices Working Group</a>]</td>
        </tr>
        <tr>
            <td>X-Device-Accept-Charset</td>
            <td>
            <a href="prov/x-device-accept-charset">prov/x-device-accept-charset</a>
            </td>
            <td>http</td>
            <td></td>
            <td>[<a href="http://www.w3.org/2005/MWI/BPWG/">W3C Mobile Web Best Practices Working Group</a>]</td>
        </tr>
        <tr>
            <td>X-Device-Accept-Encoding</td>
            <td>
            <a href="prov/x-device-accept-encoding">prov/x-device-accept-encoding</a>
            </td>
            <td>http</td>
            <td></td>
            <td>[<a href="http://www.w3.org/2005/MWI/BPWG/">W3C Mobile Web Best Practices Working Group</a>]</td>
        </tr>
        <tr>
            <td>X-Device-Accept-Language</td>
            <td>
            <a href="prov/x-device-accept-language">prov/x-device-accept-language</a>
            </td>
            <td>http</td>
            <td></td>
            <td>[<a href="http://www.w3.org/2005/MWI/BPWG/">W3C Mobile Web Best Practices Working Group</a>]</td>
        </tr>
        <tr>
            <td>X-Device-User-Agent</td>
            <td>
            <a href="prov/x-device-user-agent">prov/x-device-user-agent</a>
            </td>
            <td>http</td>
            <td></td>
            <td>[<a href="http://www.w3.org/2005/MWI/BPWG/">W3C Mobile Web Best Practices Working Group</a>]</td>
        </tr>
        <tr>
            <td>X-Mittente</td>
            <td></td>
            <td>mail</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc6109">RFC6109</a>]</td>
        </tr>
        <tr>
            <td>X-PGP-Sig</td>
            <td>
            <a href="prov/x-pgp-sig">prov/x-pgp-sig</a>
            </td>
            <td>netnews</td>
            <td></td>
            <td>[<a href="ftp://ftp.isc.org/pub/pgpcontrol/FORMAT">ftp://ftp.isc.org/pub/pgpcontrol/FORMAT</a>][<a href="https://ftp.isc.org/pub/pgpcontrol/FORMAT">https://ftp.isc.org/pub/pgpcontrol/FORMAT</a>]</td>
        </tr>
        <tr>
            <td>X-Ricevuta</td>
            <td></td>
            <td>mail</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc6109">RFC6109</a>]</td>
        </tr>
        <tr>
            <td>X-Riferimento-Message-ID</td>
            <td></td>
            <td>mail</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc6109">RFC6109</a>]</td>
        </tr>
        <tr>
            <td>X-TipoRicevuta</td>
            <td></td>
            <td>mail</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc6109">RFC6109</a>]</td>
        </tr>
        <tr>
            <td>X-Trasporto</td>
            <td></td>
            <td>mail</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc6109">RFC6109</a>]</td>
        </tr>
        <tr>
            <td>X-VerificaSicurezza</td>
            <td></td>
            <td>mail</td>
            <td></td>
            <td>[<a href="https://tools.ietf.org/html/rfc6109">RFC6109</a>]</td>
        </tr>
    </tbody>   
</table>  

#### Content-Translation-Type Header Field Values ####

<dl>
    <dt>Registration Procedure(s)</dt>
    <dd>
        <pre>Specification Required</pre>
    </dd>
    <dt>Expert(s)</dt>
    <dd>
        <pre>Nathaniel Borenstein, Nik Tomkinson</pre>
    </dd>
    <dt>Reference</dt>
    <dd>[<a href="https://tools.ietf.org/html/rfc8255">RFC8255</a>]</dd>
    <dt><br></dt>
    <dd></dd>
</dl>

<table id="table-content-translation-type-header-field-values" class="sortable">
    <thead>
        <tr style="cursor: pointer;">
            <td class="">Value </td>
            <td class="sorted">Description </td>
            <td class="">Reference </td>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>original</td>
            <td>Content in the original language</td>
            <td>[<a href="https://tools.ietf.org/html/rfc8255">RFC8255</a>]</td>
        </tr>
        <tr>
            <td>human</td>
            <td>Content that has been translated by a human translator
            or a human has checked and corrected an automated translation</td>
            <td>[<a href="https://tools.ietf.org/html/rfc8255">RFC8255</a>]</td>
        </tr>
        <tr>
            <td>automated</td>
            <td>Content that has been translated by an electronic agent
            without proofreading or subsequent correction</td>
            <td>[<a href="https://tools.ietf.org/html/rfc8255">RFC8255</a>]</td>
        </tr>
    </tbody>
</table>

<script src="https://lib.baomitu.com/jquery/1.12.4/jquery.min.js" type="text/javascript"></script>
<script src="../../../../js/sort.js" type="text/javascript"></script>
