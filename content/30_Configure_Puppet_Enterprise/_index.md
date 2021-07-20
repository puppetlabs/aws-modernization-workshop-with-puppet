---
title: "Configure Puppet Enterprise" 
chapter: true
weight: 30
---

# Configuring Puppet Enterprise

Configuring Puppet Enterprise (PE) to integrate with Relay for this workshop will leverage the same basic workflow and mechanisms you'd employ when managing resources upon arbitrary EC2 nodes hosting organization applications. We'll begin by configuring and deploying a basic [Control Repository](https://puppet.com/docs/pe/2019.8/control_repo.html) which contains all the code required to configure PE for this workshop.

1. <a name="pe-step-1"></a>Navigate to the Puppet Enterprise console, which runs over the standard HTTPS port (443)
  - Find and click on **Node groups**, found in the left side navigation panel
![Step 1](/images/30_Configure_Puppet_Enterprise/01_pe_node_groups.png)

2. <a name="pe-step-2"></a>Expand **PE Infrastructure** and click on **PE Master**
![Step 2](/images/30_Configure_Puppet_Enterprise/02_pe_node_groups_pe_master.png)

3. <a name="pe-step-3"></a>Click on **Classes**, found in the horizontal set of tabs
![Step 3](/images/30_Configure_Puppet_Enterprise/03_pe_master_classes_tab.png)

4. <a name="pe-step-4"></a>Scroll down until you find **Class: puppet_enterprise::profile::master**
  - Use the drop down menu **Parameter Name** and find **r10k_remote**
  - Set **r10k_remote** to `https://github.com/puppetlabs/aws-hol-repo.git` and click **Add to node group**
  - Now set **code_manager_auto_configure** to `true`
  - Commit changes by clicking on **Commit 2 changes**
![Step 4](/images/30_Configure_Puppet_Enterprise/04_pe_master_code_manager_config.png)

5. <a name="pe-step-5"></a>Log into your PE deployment as `puppetadmin` via SSH and run Puppet via the CLI
  - `sudo -i puppet agent -t`
![Step 5](/images/30_Configure_Puppet_Enterprise/05_pe_run_puppet_cli.png)

6. <a name="pe-step-6"></a>Once you see similar output and you're returned to a command prompt then continue to the next step
![Step 6](/images/30_Configure_Puppet_Enterprise/06_pe_run_puppet_cli_results.png)

7. <a name="pe-step-7"></a>To deploy our Control Repository we first authenticate to the PE API
  - `sudo -i puppet access login --lifetime=1y`
  - Login with credentials set during the AWS Marketplace PE deployment process
![Step 7](/images/30_Configure_Puppet_Enterprise/07_pe_get_access_token.png)

8. <a name="pe-step-8"></a>Deploy the production code environment
  - `sudo -i puppet code deploy production --wait`
![Step 8](/images/30_Configure_Puppet_Enterprise/08_pe_deploy_control_repo.png)

9. <a name="pe-step-9"></a>Import newly available classes introduced by freshly deployed Control Repository
  - Return to the PE console
  - Navigate to the **PE Master** node group
  - Find upon the page **Class definitions updated...** and click upon the **Refresh** link
![Step 9](/images/30_Configure_Puppet_Enterprise/09_pe_import_classses.png)

10. <a name="pe-step-10"></a>Add the **profile::relay** class to our **PE Master** node group
  - Select the **Classes** tab
  - In the **Add new class** field type **profile::relay**, the console will attempt to autocomplete 
  - Click on the **Add class** button
![Step 10](/images/30_Configure_Puppet_Enterprise/10_pe_add_profile_relay.png)

11. <a name="pe-step-11"></a>Provide additional data to the **profile::relay** class
  - Using the parameter drop down, add **trigger_token**
  - Set `trigger_token` to the value of the token you obtained from Relay's **puppet-report** trigger in the [Configuring Relay section, step 8]({{< ref "/20_Configure_Relay#relay-step-8" >}})
  - Commit 1 change to the **PE Master** node group
![Step 11](/images/30_Configure_Puppet_Enterprise/11_pe_commit_profile_relay.png)

12. <a name="pe-step-12"></a>Puppet agent configuration runs do no require shell access, we'll go ahead and use the PE console to initiate the run this time
  - Scroll to the top of the page and find the **Run** drop down menu
  - Select **Puppet**
![Step 12](/images/30_Configure_Puppet_Enterprise/12_pe_run_puppet_console.png)

13. <a name="pe-step-13"></a>New pane will open where you can modify the list of nodes Puppet will be ran on or change **Run options**
  - Click **Run job** to start running Puppet on our PE deployment
![Step 13](/images/30_Configure_Puppet_Enterprise/13_pe_run_puppet_job.png)

14. <a name="pe-step-14"></a>Wait for Puppet run to finish
  - Page will live update with status of Puppet run, eventually reporting **Succeeded**
  - Click on the date coded link in the **Report** column to get a view of what the Puppet run changed
![Step 14](/images/30_Configure_Puppet_Enterprise/14_pe_run_puppet_success.png)

 15. <a name="pe-step-15"></a>Review the Puppet run report
   - There may be additional changes here but the most important as those related to the configuration of Relay
![Step 15](/images/30_Configure_Puppet_Enterprise/15_pe_run_puppet_report.png)