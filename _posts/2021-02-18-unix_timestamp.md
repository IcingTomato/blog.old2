---
layout: post
title: "Let's Get the Timestamp!"
description: "How to get Timestamp by using any Language?"
comments: false
keywords: "Timestamp, Linux"
---

# Python

```python
import time
    time.time()
```

# Swift

```swift
NSDate().timeIntervalSince1970
```

# Go

```golang
import (
      "time"
    )
    int32(time.Now().Unix())
```

# Java 

```java
// pure java
    (int) (System.currentTimeMillis() / 1000)

// joda
    (int) (DateTime.now().getMillis() / 1000)
```

# JavaScript

```js
Math.round(new Date() / 1000)
```

# Objective-C

```objc
[[NSDate date] timeIntervalSince1970]
```

# MySQL

```sql
SELECT unix_timestamp(now())
```

# SQLite

```sql
SELECT strftime('%s', 'now')
```

# Erlang

```erl
calendar:datetime_to_gregorian_seconds(calendar:universal_time())-719528*24*3600.
```

# PHP

```php
// pure php
    time()

// Carbon\Carbon
    Carbon::now()->timestamp
```

# Ruby

```ruby
Time.now.to_i
```

# Shell

```shell
date +%s
```

# Groovy

```groovy
(new Date().time / 1000).intValue()
```

# Lua

```lua
os.time()
```

# .NET/C#

```csharp
(DateTime.Now.ToUniversalTime().Ticks - 621355968000000000) / 10000000
```