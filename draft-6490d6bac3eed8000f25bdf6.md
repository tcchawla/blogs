---
title: "Slack"
slug: slack

---

Slack is a popular communication platform designed to be mainly used in organizations to improve productivity. In this section, we will learn how to integrate MindsDB into your Slack Workspace.

# Setting up the Connection

To make a connection to Slack, we need a Slack API token for authentication.

If you already have the API token for Slack, feel free to skip the following steps.

Here are the steps to generate the Slack API token:

* Go to Slack App Management Dashboard.
    
* Create a new App or select an existing App.
    
* In the App Settings, go to the "OAuth & Permissions" section.
    
* Under the "Bot Token Scopes" section, add all the necessary scopes for your application. Don't worry you can add/remove later as well.
    
* Now, Install this app in your workspace.
    
* In the "OAuth Tokens & Redirect URLs" Section, copy the Bot User OAuth Access Token. This is the API token used for the authentication later.
    
* "Go to your Slack App, in order to use the Slack App which we created, we have to add the bot to the channel, in order to use the bot. for this,
    
    * Click the channel to which the bot will be used.
        
    * Go to "View Channel Details."
        
    * Select "Integrations".
        
    * Click on "Add an App".
        
    * You can see the name of the bot under the "In your workspace" Section, Go ahead and add the app to the channel.
        

Now, we can use the token which we copied from the "OAuth Tokens & Redirect URLs" Section to initialize and test our newly created Slack Bot.

Once you have completed all the mentioned steps, you should be good to go for the next steps. Now, through the MindsDB SQL Editor, we will connect to Slack with the following:

```sql
CREATE DATABASE mindsdb_slack 
WITH 
    ENGINE = 'slack', 
    PARAMETERS = { 
        "token": "<slack-bot-token>" 
    };
```

This query will create a database called `mindsdb_slack` and `channels` table automatically.

Here is how to retrieve the 10 latest messages from the channel:

```sql
SELECT messages
FROM mindsdb_slack.channels
WHERE channel="testing"
LIMIT 10;
```

However, you can also retrieve messages in alphabetical order by using:

```sql
SELECT messages
FROM mindsdb_slack.channels
WHERE channel="testing"
ORDER BY messages ASC
LIMIT 5;
```

By default, it retrieves by the order the messages were sent, unless specified ascending/descending.

Here is the query to write messages:

```sql
INSERT INTO mindsdb_slack.channels (channel, message)
VALUES
  ("testing", "It's never been that easy to build ML apps using MindsDB!");
```