---
title: "Corrective Change Exercise" 
chapter: true
weight: 40
---

# Unauthorized changes to sudo exercise

In this lab we'll enroll the additional EC2 instance you deployed while setting up prerequisites into Puppet Enterprise and start managing sudo. When sudo is managed we'll look at how our imported workflow is triggered then make a simple change to the EC2 instance to trigger a corrective change on the next Puppet run. With the sudo configuration successfully remediated, return to Relay one more time and observe the difference between this execution of our workflow vs. the previous envocation.

1. <a name="ex-step-1"></a>Navigate the **PE Agent** node group
  - Return to the **Node groups** section of the console
  - Expand **PE Infrastructure**, if still not expanded from previous steps
  - Click on **PE Agent** link
![Step 1](/images/40_Exercise/01_pe_node_group_agent.png)

2. <a name="ex-step-2"></a>Add class **profile::base**
  - The Control Repository we previous deployed contains a class named **profile::base** which will setup sudo management
  - Begin typing **profile::** and the console with autocomplete, select **profile::base** and then click **Add class**
![Step 2](/images/40_Exercise/02_pe_add_profile_base.png)

3. <a name="ex-step-3"></a>Commit chnages to **PE Agent** node group
  - There are no additional pieces of data to set for this class for click on **Commit 1 change**
![Step 3](/images/40_Exercise/03_pe_commit_profile_base.png)

4. <a name="ex-step-4"></a>Naviage to **Nodes** section via the vertical navigation bar
  - You should only see a single other node currently listed, this is the PE deployment
![Step 4](/images/40_Exercise/04_pe_nodes_section.png)

5. <a name="ex-step-5"></a>Click on the **Add nodes** button
  - Will send you a page which lists a couple ways of adding a node to inventory
![Step 5](/images/40_Exercise/05_pe_add_nodes.png)

6. <a name="ex-step-6"></a>Click on the **Install agents** button
  - Since we're working with EC2 instances, we'll choose **Install agents**
  - Puppet can also manage devices and API endpoints
![Step 6](/images/40_Exercise/06_pe_install_agents.png)

7. <a name="ex-step-7"></a>Copy command for initiating an agent install from the cli
  - To avoid setting up and distributing SSH credentials for our workshop, we'll copy the command for ***nix** under the **Install agents on the command line** section
  - This command could also be integrated into your standard provisioning workflow to ensure Puppet is installed on first boot
![Step 7](/images/40_Exercise/07_pe_copy_installer_cmd.png)

8. <a name="ex-step-8"></a>Run copied command on EC2 instance
  - SSH into the additional EC2 instance that you deployed during prerequisite setup as user **centos**
  - Paste command onto cli
![Step 8](/images/40_Exercise/08_agent_cli_run_installer_cmd.png)

9. <a name="ex-step-9"></a>Run Puppet for the first time, waiting for onboarding approval
  - With Puppet installed, initiate the first configuration run
  - Puppet will wait for you to approve the new node, checking to see if it can continue every 5 seconds
  - `sudo -i puppet agent -t --waitforcert 5`
![Step 9](/images/40_Exercise/09_agent_cli_first_run_wait.png)

10. <a name="ex-step-10"></a>Navigate to **Certificates** section of PE console
  - Return to the PE console and refresh your browser
  - There is now bee the number 1 next to **Certificates** in the vertical navigation bar
![Step 10](/images/40_Exercise/10_pe_certificates_section.png)

11. <a name="ex-step-11"></a>Select **Unsigned Certificates** tab
  - This number 1 will also be present next to **Unsigned Certificates**
  - Click on this tab
![Step 11](/images/40_Exercise/11_pe_new_certificates_tab.png)

12. <a name="ex-step-12"></a>Accept new agent certificate
  - Click on the **Accept** button
![Step 12](/images/40_Exercise/12_pe_accept_agent_cert.png)

13. <a name="ex-step-13"></a>Wait for Puppet to finish its initial run
  - Return to your SSH session and the Puppet run will have started
  - When it finishes you'll likely see events related to **Sudo::Conf**
![Step 13](/images/40_Exercise/13_agent_first_run_complete.png)

14. <a name="ex-step-14"></a>Switch to Relay to observe workflow trigger
  - Click on name of previously imported workflow
  - May currently be labled as **RUNNING**
![Step 14](/images/40_Exercise/14_relay_select_workflow.png)

15. <a name="ex-step-15"></a>Examine steps to see where workflow exits
  - Each time Puppet runs, it sends those previously observed events to the PE server, which forwards them off to any number of configured endpoints for additional processing and storage
  - Some instances of the workflow have probably already ran, the PE server is also managed by Puppet and been forwarding events
  - Click into the most recent run
  - Workflow will exit success but report a number of steps skipped
![Step 15](/images/40_Exercise/15_relay_no_changes_run.png)

16. <a name="ex-step-16"></a>Verify that no corrective changes were detected by examining step logs
  - Click on **View logs** of the **detect-changes** step
![Step 16](/images/40_Exercise/16_relay_no_changes_log.png)

17. <a name="ex-step-17"></a>Make a change to the EC2 instance's sudo configuration out of band of Puppet
  - Removing a file within the `/etc/sudoers.d` directory is sufficient
  - `sudo -i rm /etc/sudoers.d/10_puppetadmin`
![Step 17](/images/40_Exercise/17_rm_sudo_run_puppet.png)

18. <a name="ex-step-18"></a>Re-run Puppet to trigger a corrective change
  - `sudo -i puppet agent -t`
  - Output will again report events related to **Sudo::Conf** but this time you can see that they are tagged **corrective**
![Step 18](/images/40_Exercise/18_puppet_run_corrective.png)

19. <a name="ex-step-19"></a>Return to Relay again to witness the post corrective change workflow run
  - Another instance of the workflow should now be running
![Step 19](/images/40_Exercise/19_relay_changes_run.png)

20. <a name="ex-step-20"></a>Approve instance shutdown action
  - Having detected corrective changes, the workflow will eventually pause at step **Approval required**
  - This approval could be replaced with another mechanism or augmented by a chatops step to prevent having to check in on these runs periodically
  - Click on **Approve**
![Step 20](/images/40_Exercise/20_relay_approve_stop.png)

21. <a name="ex-step-21"></a>Once complete, verify which instance ID was shutdown by Relay
  - When the **ec2-stop-instances** step in complete, open its logs to see the ID of the instance it stopped
![Step 21](/images/40_Exercise/21_relay_stop_log.png)

22. <a name="ex-step-22"></a>Once shutdown, your SSH connection will also be terminated
  - When you return to your EC2 instance's SSH connection, it'll also now be terminated
![Step 22](/images/40_Exercise/22_puppet_cli_instances_stopped.png)