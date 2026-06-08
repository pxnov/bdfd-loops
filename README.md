# BDFD Global Ticking System / Automation

## Overview

This document provides a technical guide for implementing an ticking system in the BDFD (Bot Designer for Discord). The method described utilizes automated message deletion to trigger continuous code execution.

Two discord bots are required for this implementation:
- [Martine](https://martinebot.com/)
- [Autodelete Light](https://top.gg/bot/1199003582691811449)

## Implementation Steps

### 1. Server Configuration

1. Navigate to your discord server
2. Create an NSFW-designated channel
3. Configure Martine Bot with the `/autoporn` command in this channel
   - Martine Bot will automatically send content at 5-minute intervals
   - You don't have to see the contents 💔, it's bad. Just mute the channel.
4. Configure Autodelete Light Bot with `/set` command
   - Configure in the same channel as Martine Bot autoporn was set
   - Specify the deletion time interval as desired (1 second recommended)

### 2. BDFD Implementation

In your BDFD project:

1. Create a trigger using `$onDeleteMessage[channel id]`
2. Implement your code within the `$onDeleteMessage[channel id]` trigger

### 3. Execution Mechanism

The infinite loop operates as follows:
1. Martine Bot sends content every 5 minutes
2. Autodelete Light removes the content after the specified time interval
3. Each deletion triggers the `$onDeleteMessage` event in your BDFD bot
4. Your code executes upon each trigger

## Disclaimer

This implementation should be used in accordance with [Discord's Terms](https://discord.com/terms) and [BDFD's Terms](https://botdesignerdiscord.com/tos)

Node reset will not affect this as external non-bdfd bots are used.
