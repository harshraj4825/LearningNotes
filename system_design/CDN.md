## Content delivery Network
A cdn is a globally distributed of proxy servers, serving content from locations closer to the user. Generally, static files such as HTML/CSS/JS, photos, and videos are served from CDN. Although some CDNs such as 
Amazon CloudFront support dynamic content. The site's DNS resolution will tell clients which server to contact.  

Serving content from CDBs can significantly improve the performace in two ways
- Users recieve content from data centers close to them.
- Your servers do not have to server requests that the CDN fulfills

### Push CDNs
Push CDNs recieve new content whenever changes occur on your server. You take full responsibility for providing content, 
uploading directly to the CDN and rewriting URLs to point to the CDN. You can configure when content expires and when it is updated. Content is uploaded only when it is 
new or changed, minimizing traffic, but maximizing storage.  

Sites with small traffic, or sites with content that is not often change work well with push CDNs. 
Content is placed on CDNs once, instead of being re-pulled at regular intervals.  

### Pull CDNs
Pull CNNs grab new content from your server when the first user requests the content. You leave the content on your server and rewrite URLs to point to the CDN. 
This result is a slower request until content is cached on the CDN.  

A time-to-live (TTL) determine how long content is cached. Pull CDNs minimize storage space on the CDN, but can create redundant traffic if 
files expire and are pulled before they have actually changed. 
Sites with heavy traffic work well with pull CDNs, as traffic is spread out more evenly with only recently-requested content remaining on the CDN.  

#### Disadvantage(s): CDN
- CDN costs could be significant depending on traffic, although this should be wieghed with additional costs you wound incur not using a CDN.
- Content might be stale if it is updated before the TTL expires it.
- CNDs require changing URLs for static content to point to the CDN.
