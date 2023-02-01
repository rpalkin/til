---
title: "My Awesome List of Golang tools and libraries"
date: 2023-02-01T20:07:13+03:00
weight: 1
tags: ["golang"]
author: "Me"
# author: ["Me", "You"] # multiple authors
showToc: true
TocOpen: false
draft: false
hidemeta: false
comments: false
description: "Desc Text."
canonicalURL: "https://canonical.url/to/page"
disableHLJS: true # to disable highlightjs
disableShare: false
disableHLJS: false
hideSummary: false
searchHidden: true
ShowReadingTime: true
ShowBreadCrumbs: false
ShowPostNavLinks: true
ShowWordCount: true
---

## Http client

- https://github.com/go-resty/resty
```go
    httpClient := resty.New()
	httpClient.SetBaseURL("https://baseurl.com/")
	httpClient.SetBasicAuth(key, secret)
	
    response := ResponseInterface{}
    _, err = httpClient.R().
		SetResult(&response).
		SetPathParam("param", paramValue).
		Get("api/method/{param}")
	
	spew.Dump(response)
```