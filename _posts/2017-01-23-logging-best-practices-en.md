---
layout: post
title: "Logging Best Practices for Java"
date: 2017-01-23 06:39:00 +6390
categories: logging
lang: en
ref: logging-best-practices-for-java
---

## **Summary**
This reference document shows the logging best practice for java

## **Description**
Logging subsystem provides facilities for capturing, recording and reporting events which occur within the OpenDaylight system. These events are the primary means of system diagnostics and troubleshooting, serving a wide audience including automated monitoring systems, operators, administrators, support personnel and development engineers.

In order to provide a 'single system' experience, all software components should follow same basic rules for interfacing with the logging system. While it is not practical to force these rules on the various third parties, they should to be followed by all newly-developed components.

## **Contents**
1. [Why we need logging in Java?](#why-we-need-logging-in-java)
1. [How logging in Java affects performance?](#how-logging-in-java-affects-performance)
1. [Message levels](#message-levels)
1. [Logger instances](#logger-instances)
1. [Use parameterized logging](#use-parameterized-logging)
1. [Provide useful event context](#provide-useful-event-context)
1. [What should you log](#what-should-you-log)
1. [Tune your pattern](#tune-your-pattern)
1. [Log method arguments and return values](#log-method-arguments-and-return-values)

## **Why we need logging in Java?**
[Go to Contents Table](#contents)

## **How logging in Java affects performance?**
[Go to Contents Table](#contents)

## **Message levels**
[Go to Contents Table](#contents)

## **Logger instances**
[Go to Contents Table](#contents)

## **Use parameterized logging**
[Go to Contents Table](#contents)

## **Provide useful event context**
[Go to Contents Table](#contents)

## **What should you log?**
[Go to Contents Table](#contents)

## **Tune your pattern**
[Go to Contents Table](#contents)

## **Log method arguments and return values**
[Go to Contents Table](#contents)

## **Watch out for external systems**
[Go to Contents Table](#contents)

## **Log exceptions properly**
[Go to Contents Table](#contents)

## **Logs easy to read, easy to parse**
[Go to Contents Table](#contents)
