# BDFD Infinite Loop Implementation Guide

## Overview

This document provides a technical guide for implementing an infinite loop in the BDFD (Bot Designer for Discord) programming language. The method described utilizes automated message deletion to trigger continuous code execution.

## Prerequisites

Two Discord bots are required for this implementation:
- Martine Bot
- Autodelete Light Bot

## Implementation Steps

### 1. Server Configuration

1. Navigate to your private Discord server
2. Create an NSFW-designated channel
3. Configure Martine Bot with the `/autoporn` command in this channel
   - Martine Bot will automatically send content at 5-minute intervals
4. Configure Autodelete Light Bot with `/set channel` command
   - Specify the deletion time interval as desired

### 2. BDFD Implementation

In your BDFD project:

1. Create a trigger using `$onDeleteMessage[channel id]`
   - Note: Direct channel ID input is required
   - Avoid using `$getServerVar[channel id]` as it will not function properly
   - Ensure this is set in a different channel from where Martine and Autodelete Light are configured

2. Implement your code within the `$onDeleteMessage[channel id]` trigger
   - Recommended functions: `$sendEmbedMessage`, `$channelSendMessage`

### 3. Execution Mechanism

The infinite loop operates as follows:
1. Martine Bot sends content every 5 minutes
2. Autodelete Light Bot removes the content after the specified time interval
3. Each deletion triggers the `$onDeleteMessage` event in your BDFD bot
4. Your code executes upon each trigger

## Technical Notes

This method creates a pseudo-infinite loop by leveraging automated message creation and deletion as trigger events. The execution frequency depends on the deletion time interval configured in Autodelete Light Bot.

## Disclaimer

This implementation should be used in accordance with Discord's Terms of Service and applicable platform policies. Ensure your use case complies with all relevant guidelines and regulations.
