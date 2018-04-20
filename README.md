# Introduction

The purpose of this package is to generally provide "test data" for the bookwerx-* family of packages.

# The Problem

**bookwerx-core** provides an HTTP API which implements a bookkeeping engine for the rest of the family.  We want to somehow test this. One important part of its testing is an integration test.  In this integration test we want to make a long sequence of CRUD operations.  In fact, this sequence of operations is so long and tedious that it becomes difficult to wrap our heads around it and feel confident that the sequence is good.

**bookwerx-ui** provides an HTTP API which provides a UI to enable [a desperate fool at the end of his pitiful rope](https://www.youtube.com/watch?v=87w655s3xKc#t=2m27s) to do these same operations manually.  This also ought to be tested.  We certainly want to be able to click our way through the UI, enter form fields, and monitor the results.  In fact, whatever we do in the **bookwerx-core** integration testing ought to be done in the **bookwerx-ui** integration testing.

In both cases we will ultimately want to send the exact same sequence of HTTP requests to **bookwerx-core**.  But in the case of the UI we want to do that by first clicking our way through the UI. The naive approach would be to just make two systems of tests. However, because both tests want the same sequence of HTTP requests, and because the ideal system is so big and tedious and of necessity carefully considered, and because we generally wish to keep our code DRY, I want some system to generally "script" this test that both packages can use.

**bookwerx-core** can thus follow the script and do what's relevant to it, such as perhaps ignoring UI related gyrations, while **bookwerx-ui** can follow the same script and do what's relevant to it.

# The Solution

**bookwerx-core** therefore provides "universalIntegrationTest" which everybody can use.