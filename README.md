# BDFD Infinite Loop Implementation Guide

## Overview

This document provides a technical guide for implementing an infinite loop in the BDFD (Bot Designer for Discord) programming language. The method described utilizes automated message deletion to trigger continuous code execution.

## Prerequisites

Two Discord bots are required for this implementation:
- [Optional] Martine (https://martinebot.com/)
- Autodelete Light (https://discord.com/oauth2/authorize?client_id=1199003582691811449)

## Implementation Steps

### 1. Server Configuration

1. Navigate to your private Discord server
2. Create an NSFW-designated channel
3. Configure Martine Bot with the `/autoporn` command in this channel
   - Martine Bot will automatically send content at 5-minute intervals
4. Configure Autodelete Light Bot with `/set channel` command
   - Specify the deletion time interval as desired

or

1. Navigate to your private Discord server
2. Create a channel where the loop will be implemented
3. Configure Autodelete Light Bot with `/set channel` command
4. Set the deletion interval to greater than 10 seconds (recommended)
   - This timing is critical to ensure proper functionality

### 2. BDFD Implementation

In your BDFD project:

1. Create a trigger using `$onDeleteMessage[channel id]`
   - Note: Direct channel ID input is required
   - Avoid using `$getServerVar[channel id]` as it will not function properly
   - Ensure this is set in a different channel from where Martine and Autodelete Light are configured

2. Implement your code within the `$onDeleteMessage[channel id]` trigger
   - Recommended functions: `$sendEmbedMessage`, `$channelSendMessage` instead of `$title`, `$description` etc.

or

1. Create a trigger using `$onDeleteMessage[channel id]`
   - Use the channel ID where Autodelete Light is configured

2. Implement the following code within the trigger:
   ```
   $channelSendMessage[channelID;**Loop Trigger**!]
   ```
   - Replace `channelID` with the actual ID of the channel where Autodelete Light is configured
   - This message will serve as the trigger for the next deletion cycle

### 3. Execution Mechanism

The infinite loop operates as follows:
1. Martine Bot sends content every 5 minutes / Your BDFD bot sends "**Loop Trigger**!" message to the configured channel
2. Autodelete Light Bot removes the content after the specified time interval
3. Each deletion triggers the `$onDeleteMessage` event in your BDFD bot
4. Your code executes upon each trigger
5. The cycle repeats indefinitely

## Technical Notes

This method creates a pseudo-infinite loop by leveraging automated message creation and deletion as trigger events. The execution frequency depends on the deletion time interval configured in Autodelete Light Bot.

## Disclaimer

This implementation should be used in accordance with Discord's Terms of Service and applicable platform policies. Ensure your use case complies with all relevant guidelines and regulations.




# BDFD Infinite Loop Implementation Guide - Alternative Method

## Overview

This document provides an alternative technical approach for implementing an infinite loop in the BDFD (Bot Designer for Discord) programming language. This simplified method utilizes a single bot and message deletion triggers.

## Prerequisites

One Discord bot is required for this implementation:
- Autodelete Light Bot

## Implementation Steps


### 2. BDFD Implementation

In your BDFD project:


### 3. Execution Mechanism

The infinite loop operates as follows:
1. 
2. Autodelete Light Bot removes the message after the specified time interval (>25 seconds)
3. Each deletion triggers the `$onDeleteMessage` event in your BDFD bot
4. Your code executes, sending another "**Loop Trigger**!" message

6. 
## Technical Notes

This method creates a self-sustaining loop by:
- Having your BDFD bot send a message
- Relying on Autodelete Light to remove that message
- Using the deletion event to trigger the next message

The 25-second minimum interval is recommended to ensure:
- Proper execution timing
- Prevention of rate limiting
- Stability of the loop mechanism

This approach requires fewer resources than the two-bot method and provides more direct control over the loop execution.

Would you like me to provide additional code examples or explain any specific aspects of this implementation in more detail?
