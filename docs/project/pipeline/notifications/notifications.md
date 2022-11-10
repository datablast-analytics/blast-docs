# Notifications
Blast Scheduler sends notifications about pipeline status. There are 2 notification channels available:
- [Slack](slack.md)
- [Discord](discord.md)

You can specify which channels you want to use in your `pipeline.yml` file. There are 4 arguments to specify for every channel you want to receive notifications, :

- `name`: Name for the channel.
- `connection`: Connection ID of the channel.
- `success`: Message to be formatted with relevant information and sent to the specified channel when pipeline succeeds.
- `failure`:  Message to be formatted with relevant information and sent to the specified channel when pipeline fails.

_**Note**: you don't have to define success and failure in every case_

A simple notification setup in your `pipeline.yml` looks like this:

```yaml
notifications:
    slack:
        - name: data-team
          connection: "slack-data-team"
          success: ":tada: Pipeline has finished successfully!"
          failure: ":red_circle: Pipeline has failed!"

    discord:
        - name: marketing-team    
          connection: "discord-marketing-team"
          failure: ":red_circle: Pipeline has failed!"
```
