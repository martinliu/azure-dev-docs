---
title: Configure logging in the Azure SDK for Java
description: An overview of the Azure SDK for Java concepts related to logging
ms.date: 02/02/2021
ms.topic: conceptual
ms.custom: devx-track-java
author: KarlErickson
ms.author: srnagar
---

# Configure logging in the Azure SDK for Java

This article provides an overview of how to enable logging in applications that make use of the Azure SDK for Java. The Azure client libraries for Java have two logging options:

* A built-in logging framework for temporary debugging purposes.
* Support for logging using the [SLF4J](https://www.slf4j.org/) interface.

We recommend that you use SLF4J because it's well known in the Java ecosystem and it's well documented. For more information, see the [SLF4J user manual](https://www.slf4j.org/manual.html).

This article links to other articles that cover many of the popular Java logging frameworks. These other articles provide configuration examples, and describe how the Azure client libraries can use the logging frameworks.

Whatever logging configuration you use, the same log output is available in either case because all logging output in the Azure client libraries for Java is routed through an azure-core `ClientLogger` abstraction.

The rest of this article details the configuration of all available logging options.

## Default logger (for temporary debugging)

As noted, all Azure client libraries use SLF4J for logging, but there's a fallback, default logger built into Azure client libraries for Java. This default logger is provided for cases where an application has been deployed, and logging is required, but it's not possible to redeploy the application with an SLF4J logger included. To enable this logger, you must first be certain that no SLF4J logger exists (because it will take precedence), and then set the `AZURE_LOG_LEVEL` environment variable. The following table shows the values allowed for this environment variable:

| Log Level              | Allowed Environment Variable Values     |
|------------------------|-----------------------------------------|
| VERBOSE                | "verbose", "debug"                      |
| INFORMATIONAL          | "info", "information", "informational"  |
| WARNING                | "warn", "warning"                       |
| ERROR                  | "err", "error"                          |

After the environment variable is set, restart the application to enable the environment variable to take effect. This logger will log to the console, and doesn't provide the advanced customization capabilities of an SLF4J implementation, such as rollover and logging to file. To turn the logging off again, just remove the environment variable and restart the application.

## SLF4J logging

By default, you should configure logging using an SLF4J-supported logging framework. First, include a relevant SLF4J logging implementation as a dependency from your project. For more information, see [Declaring project dependencies for logging](http://www.slf4j.org/manual.html#projectDep) in the SLF4J user manual. Next, configure your logger to work as necessary in your environment, such as setting log levels, configuring which classes do and do not log, and so on. Some examples are provided through the links below, but for more detail, see the documentation for your chosen logging framework.

## Next steps

Now that you've seen how logging works in the Azure SDK for Java, consider reviewing the links below for guidance on how to configure some of the more popular Java logging frameworks to work with SLF4J and the Java client libraries:

* [java.util.logging](logging-jul.md)
* [Logback](logging-logback.md)
* [Log4J](logging-log4j.md)
