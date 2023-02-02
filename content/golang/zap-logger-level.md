---
title: "Zap Logger Level"
date: 2023-02-02T18:06:06+03:00
tags: ["golang", "zap"]
author: "Me"
showToc: false
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
ShowRssButtonInSectionTermList: true
---

## Init zap logger with level

```go
import "go.uber.org/zap"

loggerCfg := zap.NewProductionConfig()
level := zap.InfoLevel
if err := level.Set(LevelString); err != nil {
    panic(err)
}
loggerCfg.Level = zap.NewAtomicLevelAt(level)
zapLogger, err := loggerCfg.Build()
if err != nil {
    panic(err)
}
zap.ReplaceGlobals(zapLogger)
```