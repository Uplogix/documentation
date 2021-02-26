<!-- 5.4 -->

# Overview

Monitors gather data, in some cases by running user-defined tests; and they may include rules to evaluate and respond to the data.

A rule specifies at least one condition to evaluate, and at least one action to take if the set of conditions evaluates true. Rules may also include a time element.

Rules can be grouped together into rule sets. This simplifies the process of creating monitors.

# Working with rules

<div class='ucc' />Inventory > Automation > Rules</div>

Rules can be centrally managed from the Control Center. Like privileges and preferences, rules edited at the inventory group level are inherited by child groups and Local Managers. Rules edited at the Local Manager level only apply to that Local Manager.

To access the Rules page, click *Rules* from the Automation menu at an Inventory Group detail or Local Manager Summary page. New rules can be created and existing rules can be edited.
 
![Uplogix Control Center - View Rules](http://uplogix.com/support/docs/img/5.4/uplogix-control-center-local-manager-rules-view.png)

Click **Add** to create a new rule. This is equivalent to issuing the **config rule** command from the Local Manager command line.

> Do not use spaces in the rule name.

The **Edit Rule** page contains drop-down menus and lists of the same options available from the rules editor within the Local Manager command line.

![Uplogix Control Center - Create Rules](http://uplogix.com/support/docs/img/5.4/uplogix-control-center-rules-create.png)

Edit conditions manually in the Conditions text box or add a new condition using the drop-down menus shown below. Four different menu sets cover the condition types for rules. As each condition is added, the text changes to reflect the new conditions.

Alarms and events are defined using drop-down items and free text fields.

Tasks can be manually edited or specified with the selections on this page.

Click *Save* at the bottom of the page to create the rule. Select *Force update on children* to force Local Managers to update a previously inherited rule.

# Working with rule sets

<div class='ucc' />Inventory > Automation > Rule Sets</div>

Some rules are often used together. Therefore, it may be convenient to group them into rule sets. When creating monitors, available rules and rule sets are presented together.

Click *Rule Sets* from the Automation menu on a group detail or Local Manager Summary page.

![Uplogix Control Center - View Rule Sets](http://uplogix.com/support/docs/img/5.4/uplogix-control-center-rulesets-view.png)

Existing rule sets are listed on the Rule Sets page.  To create a rule set, click *Add*. In the Create Rule Set screen, provide a name and (optionally) a brief description for the rule set.
 
![Uplogix Control Center - Create Rule Sets](http://uplogix.com/support/docs/img/5.4/uplogix-control-center-rulesets-create.png)

Select the first rule from the list of available rules, and click *add rule*.

Select the relationship (AND; OR) of the first rule to the second rule from the list to the left, then select the second rule.
 
Continue until all the desired rules have been added to the rule set. Click *Save* to save the rule set. The new rule set is listed on the View Rule Sets page.
 
#Promoting rules and rule sets

<div class='ucc' />Inventory > Automation > Rules</div>
<div class='ucc' />Inventory > Configuration > Rule Sets</div>

Rules can be promoted to different levels in the Inventory hierarchy using the promote feature. Select the rule(s) for promotion and click the **Promote** button. Select the inventory group level to promote the rule(s) and make appropriate promotion selections:

- **Overwrite existing rule**:  Overwrites rule(s) with the same name in the inventory group level where you are promoting a rule(s).
- **Force update on children**:  Overwrites rule(s) with the same name in all inventory groups and Local Managers below the selected group.

When finished with selections, click the **Promote to Group** button.
 
# Scheduling monitors

<div class='ucc' />Inventory > Local Manager > Port > Schedule Task </div>

A monitor is a type of scheduled task. Monitors gather data and may apply rules to interpret and respond to the data. Monitors are created from the port pages on individual Local Managers.

To create a monitor, click *Schedule* from the Port Detail page.

Select *Monitor* from the list of tasks and click *Next*.

On the *Parameters* page, choose the type of monitor. If it is an interface monitor, specify the interface to be monitored - for example, GigabitEthernet0/1.

The monitor can be set up without adding rules. The Local Manager gathers and stores the data without acting on it. To do this, click *Next* to go to the scheduling page.

To create a monitor that uses rules to interpret and respond to the data as it is gathered, select a rule from the list of available rules and click *Add Rule*.

To add another rule, select the rule and its relation to the rule already added. Then click *Add Rule*.

On the *Frequency* page, specify the schedule for this monitor and optionally provide a brief description.

Click *Save*. The monitor runs as scheduled and appears on the Scheduled Tasks page.
 
> The default interval for monitors is 30 seconds. However, this interval can be changed.

# Canceling monitors

To cancel a monitor, go to the *Scheduled Tasks* page. Locate the monitor to be canceled and click the *Cancel* link. The canceled monitor continues to be shown but is struck out on the Scheduled tasks list.