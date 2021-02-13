+++
title = "Capsule"
date = 2019-01-20
[taxonomies]
tags = ["C#", "Azure","React","Webpack","Blob Storage","Azure Functions","Shared Access Signatures"]
[extra]
github="https://github.com/PhilipK/XMinutes"
image="../static/images/blob.png"
description="A service for sharing content but only for a certain set of time."
+++

A small service for sharing content but only for a certain set of time.

## SAS

In Azure Blobstorage you can upload some data and then create a Shared Access Signatures (SAS) for the content. Think of an SAS as a token, that is only available for a limited set of time.
The idea of Capsule is that you can upload content but also choose in which period of time it is accessible. This could be useful for stuff like: Giving digital presents, sharing exam assignments, or setting a time limit for how long content should be available (and be deleted after.).

The system worked, and I made a small React UI interface for the solution. I guess that I didn't do more with this Capsule because I didn't really see it as something that would have a lot of "business potential", so I just open sourced it for others to see instead.
