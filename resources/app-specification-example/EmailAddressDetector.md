---
name: Email Address Detector
description: Detects email addresses within Jira work item comments.
---

# App Requirements

This app detects email addresses within Jira work item comments.

## Functional Requirements

### Problem Statement

For privacy reasons, an organisation's policy prevents personal email addresses from being entered into
Jira work item comments.

### Solution Overview

Create a Forge app that detects when new comments are created that contain personal email addresses and responds by adding a comment to the work item that indicates that the comment has been removed.

### Definitions

A personal email address is an email address that relates to a single real person rather than a role, function or group within an organisation. An example of a personal email address is joe@acme.com. An example of a non-personal email address is info@acme.com. The allowed non-personal email address prefixes are info, contact, admin, enquiries and sales.

### Generic App Requirements

See GenericAppRequirements.md for generic app requirements.

### Functional Requirements

The app must listen to the creation of new comments on Jira work items by subscribing to the `avi:jira:commented:issue` event.

The app must not process comments that are added by the app itself. To achieve this, the app's manifest can specify `ignoreSelf: true` in the `filter` section of the `trigger` module.

When a comment is created, the app must detect if it contains any personal email addresses.

If a comment is detected that contains personal email addresses, the app must remove the comment and add a new comment to the work item that indicates that the comment has been removed.

The app may use a regular expression to detect personal email addresses.

When email addresses are being detected in Atlassian Document Formatted (ADF) objects, the email addresses need to be detected in text nodes at any nesting depth, not just within paragraphs at the top level of the ADF object. A simple way to achieve this is by detecting if a node has a "content" property which is an array, and of so, inspecting the content array nodes.

When a personal email addresses is detected in a comment, the app must add a reply comment indicating that the personal email addresses need to be removed from the comment.

### Non-functional Requirements

None.
