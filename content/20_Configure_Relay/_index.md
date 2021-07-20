---
title: "Configuring Relay by Puppet" 
chapter: true
weight: 20
---

# Configuring Relay by Puppet

1. <a name="relay-step-1"></a>Relay workflows can easily be imported from the [Library](https://relay.sh/library/) or any publically accesible web link
  - Click on the below link to open the Relay workflow import wizard
  - [Puppet Enterprise Unauthorized Sudo Configuration Change](https://app.relay.sh/create-workflow?workflowName=puppet-unauthorized-sudo-fencer&initialContentURL=https://raw.githubusercontent.com/ody/relay-workflows/puppet-ec2-corrective-only/puppet-shutdown-ec2/puppet-shutdown-ec2.yaml)
  - Click on the **Create Workflow** button
![Step 1](/images/20_Configure_Relay/01_relay_import_workflow.png)

2. <a name="relay-step-2"></a>When a new workflow is imported it will inform you of the need to define additional pieces of information
  - Click on the **Fill in missing secrets** link
![Step 2](/images/20_Configure_Relay/02_relay_missing_secrets.png)

3. <a name="relay-step-3"></a>Add a new AWS connection by clicking on the "**+**" next to **my-aws-account**
![Step 3](/images/20_Configure_Relay/03_relay_add_connection.png)

4. <a name="relay-step-4"></a>A **Setup up you AWS connection** pane has opened, add here access and secrets keys for a user which has access to EC2 and click *Save*
![Step 4](/images/20_Configure_Relay/04_relay_connection_details.png)

5. <a name="relay-step-5"></a>Back at the **Workflow configuration** pain, scroll down to the **Secrets** section and click again on the "**+**" next to **awsRegion**
![Step 5](/images/20_Configure_Relay/05_relay_add_secret.png)

6. <a name="relay-step-6"></a>To keep the workshop simple, set this as the same region you deployed Puppet Enterprise to
![Step 6](/images/20_Configure_Relay/06_relay_secret_details.png)

7. <a name="relay-step-7"></a>Relay workflows can be triggered in several ways, one of is a [Push trigger](https://relay.sh/docs/using-workflows/using-triggers/#push-triggers)
  - The [Receive Puppet report](https://relay.sh/triggers/-/puppet-report) is what makes today's workshop possible
![Step 7](/images/20_Configure_Relay/07_relay_triggers.png)

8. <a name="relay-step-8"></a>Push triggers generate a workflow specific authentication token
  - Save the token for later, we'll use it to configure Puppet Enterprise
![Step 8](/images/20_Configure_Relay/08_relay_trigger_token.png)

