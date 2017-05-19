Use this [notification](http://rundeck.org/docs/developer/notification-plugin-development.html)
plugin to send [alert](https://www.opsgenie.com/docs/web-api/alert-api#createAlertRequest)
events to your [OpsGenie](https://www.opsgenie.com) service.

The plugin requires one parameter:

* subject: This string will be set as the description for the generated incident.

Context variables usable in the subject line:

* `${job.status}`: Job execution status (eg, FAILED, SUCCESS).
* `${job.project}`: Job project name.
* `${job.name}`: Job name.
* `${job.group}`: Job group name.
* `${job.user}`: User that executed the job.
* `${job.execid}`: Job execution ID.

## Installation

Copy the groovy script to the plugins directory:

    cp src/OpsGenieNotification.groovy to $RDECK_BASE/libext

and start using it!

## Configuration

The plugin only requires the 'service_key' configuration entry. There are two optional configurations if you send requests through an egress proxy.

* service_key: This is the API Key to your service.

Configure the service_key in your project configuration by
adding an entry like so: $RDECK_BASE/projects/{project}/etc/project.properties

    project.plugin.Notification.OpsGenieNotification.service_key=xx123049e89dd45f28ce35467a08577yz

Or configure it at the instance level: $RDECK_BASE/etc/framework.properties

    framework.plugin.Notification.OpsGenieNotification.service_key=xx123049e89dd45f28ce35467a08577yz

* proxy_host (optional): Your egress proxy host.
* proxy_port: Required if proxy_host is set. The port the network egress proxy accepts traffic on.

These can be configured at the project level. 
Most likely this needs to be configured at the instance level: $RDECK_BASE/etc/framework.properties

    framework.plugin.Notification.OpsGenieNotification.proxy_host=foo.example.net
    framework.plugin.Notification.OpsGenieNotification.proxy_port=3128