---
title: DevOpsTips
date: 2024-04-16 19:34:40
tags: DevOps
---

## SpingBoot3 

### hot deployment

1. add maven dependencies:

```reStructuredText
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-devtools</artifactId>
            <optional>true</optional>
        </dependency>
```

2. idea => settings => Build => Compiler

allow "Build Project Automatically"

3. idea => settings =>Advanced Settings => Compiler

allow auto-make to start even if developed application is currently running
