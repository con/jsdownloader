# jsdownloader

The summary from a web-technology ignorant @yarikoptic:

Data is getting more and more distributed.  Centralized data archives (e.g. http://openneneuro.org, http://dandiarchive.org) often offload actual data storage to services such as AWS S3, while tracking data availability internally in a relational database or other structure (e.g. git-annex, dvc). Data distributions such as http://datasets.datalad.org provide access from a wide range of data storage backends using such tools as git-annex to orchestrate registration and management of data from those external data pools.  It is also not unprecedented to have the same file available from multiple data storage pools, which is great to guarantee availability and take advantage of "data locality" (e.g. use S3 sources while already in the cloud).  Then pretty much every such centralized archive aims to provide naive users with a "Download" button on their web portals, to facilitate simple download.  Examples would include OpenNeuro, BALSA in neuroimaging domain.

## The desired solution

a JS "Downloader" library. To avoid bottle neck of a single "central archive server", ideal "Download"er needs to provide download of individual files on a client side (browser).  I think it would be great if there just was a JS library we all could use to provide needed functionality -- it would help to reinvent the wheel in each project.  I think such helper would need a simple input of a list of 

    "path": [candidate_urls]

entries (where to download to, and from where), and it would take care about delivering those files to the user (after possibly asking a local path where to save it).  Some features I see being needed and/or desired:

- on the fly generation of a .zip-ball streaming individual files from those urls
   - ideally such .zip-ball should be reproducible given the same list (given that remote urls content does not change), so should take care about having deterministic mtime (e.g. the latest mtime of individual files or smth like that)
- not sure if easily possible -- should allow for non-zip'balled download of collection of files (constructing desired directories where needed)
- if present, remote URL's modification times should be represented (questionable in case of multiple URLs - but could sense)
- should reuse authenticated in that browser sessions (e.g. URLs coming from a LORIS server session)
- should be resilient to interrupted downloads
- ideally should allow for parallel download

I wonder if such a library might exist already or what technologies could be used to facilitate establishing such a library.

## Considerations of known limitations etc

- data hosting sites might need to configure [Cross-Origin Resource Sharing (CORS)](https://enable-cors.org/) settings to allow other sites (centralized archives) to enable access to their data from JS client.  It is doable.
- MORE??? **Please contribute here and above ;)**