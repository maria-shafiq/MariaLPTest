---
title: Introduction

---
<!--Introduction-->

JSON (JavaScript Standard Object Notation) is a standard format used for exchanging between applications or over the internet. It is popular because almost all programming languages have at least one library to support it.

It is presented in a human-readable format making it easy for developers to work with it.

In Go, JSON is handled using the [JSON standard library](https://pkg.go.dev/encoding/json). You’ll encounter two types of data when working with JSON:

- Structured data
- Unstructured data

In this scenario, we’ll learn how to handle JSON data in Go applications. We’ll separate this into two separate parts:

- Unmarshaling JSON data: conversion from JSON format
- Marshaling to JSON data: conversion to JSON format

Let’s start with Unmarshaling JSON.