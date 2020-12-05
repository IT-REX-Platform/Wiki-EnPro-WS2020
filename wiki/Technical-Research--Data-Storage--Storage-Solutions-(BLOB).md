todo

- (db. vs. fs)

- for how long is data retained? do we perform cleanups?

---

# MinIO

[MinIO](https://min.io/) is an Object Storage solution that we've evaluated and deemed feasible for our purposes (storing and holding user uploads, primarily lecture recordings).
It is very portable and can be hosted locally, via Docker or on S3, which would support scaling up in the future.
We've built a prototype in Java/Spring that receives a user upload and streams it to a freely configurable MinIO instance.
Listing directories (so-called buckets) and downloading (streaming) files has also been implemented.

As this has the potential to save us some trouble as far as designing and implementing a custom storage solution goes, it is quite attractive and should definitely be taken into consideration.  
A good chunk of our security implications checklist on storing user uploads will likely be rendered obsolete as well.
