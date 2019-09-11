# Rollbar xMatters Integration

Trigger an xMatters Flow to alert xMatters groups and users when Rollbar items meet specific conditions. 
- __Assign__ a user to Rollbar items from xMatters alert.
- __Resolve__ Rollbar items from xMatters alert.
- __Mute__ Rollbar items from xMatters alert.
- __Resume__ Rollbar items from xMatters alert
- __Get Deploys__ from xMatters alert.
- __Run RQL__ from xMatters alert.
- __Get Results__ Check the status of recent Rollbar RQL and get results of the RQL in xMatters.
- Easily add additional integrations to your xMatters Flow.

<kbd>
  <img src="https://github.com/xmatters/xMatters-Labs/raw/master/media/disclaimer.png">
</kbd>

# Pre-Requisites

- Rollbar [https://rollbar.com](https://rollbar.com)
- xMatters account - If you don't have one, [get one](https://www.xmatters.com)!

# Files

- [xMatters Rollbar Communication Plan](Rollbar.zip)

# How it works

__This integration has the following Forms/Flows__:


- __Rollbar Alert__: 
        
        
    - __Inbound HTTP Trigger for Rollbar__:

            Creates an xMatters event on Rollbar:
            - __occurrence__
            - __new_item__
            - __exp_repeat_item__
            - __reopened_item__
            - __reactivated_item__. 

            When xMatters receives an inbound Rollbar webhook for __resolved_item__ 
            all matching xMatters events will be terminated.
        
        <kbd>
            <img src="/media/inbound_flow.png" width="600">
        </kbd>
        <br><br>   
        
        __Response Options__:
        
            - __ESCALATE__: Escalates xMatters event to next oncall member.   
            - __ASSIGN__: Assign a user to Rollbar items from xMatters alert.
            - __RESOLVE__: Resolve a Rollbar item from xMatters alert.
            - __MUTE__: Mute a Rollbar item from xMatters alert. This will stop additional occurances from notifying xMatters.
            - __RESUME__: Resume a Rollbar item from xMatters alert
            - __GET DEPLOYS__: Gets last 3 most recent deploys in Rollbar from xMatters alert.
            - __RUN RQL__: Runs a Rollbar Query Language command from xMatters alert.

    - __Outbound Response Triggers__: 

            Triggers include ESCALATE, ASSIGN, RESOLVE, MUTE, RESUME, GET DEPLOYS and RUN RQL.
         
        <kbd>
            <img src="/media/outbound_flow.png" width="600">
        </kbd>
        <br><br>

- __Recent Deploys__: 
 
    Creates xMatters event with the last 3 recent deploys in Rollbar.
     
    __Response Options__: -none-

    __Flow__: -none-

- __Create New RQL Job__: 
 
    Create xMatters event for a New RQL Job.
 
    __Response Options__:
    - __GET RESULTS__: Gets the results from Rollbar to the related RUN RQL response trigger.

    __Flow__:
    - Outbound Response Triggers for GET RESULTS.


    <kbd>
        <img src="/media/get-results.png" width="600">
    </kbd>
    <br><br>
        
        
 
 - __RQL Results__: 
 
    Create xMatters event with the results from the related RQL Job
 
    - __Response Options__: -none-

    - __Flow__: -none-
 
 
 
 - __RQL Results Not Ready__: 
 
    Create xMatters event notifying user the RQL results are not ready and to try again later.

    - __Response Options__:
    
        - __GET RESULTS__: Gets the results from Rollbar to the related RUN RQL response trigger.

    - __Flow__:
    
        - Outbound Response Triggers for GET RESULTS.

    <kbd>
        <img src="/media/get-results.png" width="600">
    </kbd>
    <br><br>

            
        
<kbd>
    <img src="/media/flow_list.png" width="600">
</kbd>
<br><br>




__Easily add additional integrations to your xMatters Flow__

<kbd>
    <img src="/media/customize-steps.png" width="600">
</kbd>
<br><br>


__This integration has the following xMatters Flow Steps for Rollbar Included__:

- Create a Rollbar RQL Job (Rollbar)
- Get Rollbar Recent Deploy (Rollbar)
- Get Rollbar RQL Status (Rollbar)
- Get Rollbar Single User By Name (Rollbar)
- Parse Rollbar RQL Results (Rollbar)
- Update Rollbar Item Status (Rollbar)
- Get Events (xMatters)
- Change the Status of all Events (xMatters)


<kbd>
    <img src="/media/flow-steps.png" width="600">
</kbd>
<br><br>




# xMatters Configuration

### Create an xMatters Integration User

Although this step is not required, it is recommended. This will enhance security and ensure the integration does not unintentionally break when a password is changed.

**Note**: If you are installing this integration into an xMatters trial instance, you don't need to create a new user. Instead, locate the "Integration User" sample user that was automatically configured with the REST Web Service User role when your instance was created and assign them a new password. You can then skip ahead to the next section.

**To create an integration user:**

1. Log in to the target xMatters system.
2. On the **Users** tab, click the **Add New User** icon.
3. Enter the appropriate information for your new user.
   Example User Name **API_User**
4. Assign the user the **REST Web Service User** role.
5. Click **Save**.

<br><br>

## Import and Configure the xMatters Communication Plan

To import the communication plan:

1. In the target xMatters system, on the **Developer** tab, click **Import Plan**.
2. Click **Browse**, and then locate the downloaded communication plan: [Rollbar](Rollbar.zip)
3. Click **Import Plan**.
4. Once the communication plan has been imported, click **Plan Disabled** to enable the plan.
5. In the **Edit** drop-down list, select **Access Permissions**.

<kbd>
    <img src="/media/access_permissions.png" width="300">
</kbd>
<br><br>

6. Add the **API_User** or Make the Plan **Accessible by All**.
7. **Save Changes**.

<kbd>
    <img src="/media/set_access_permissions.png" width="300">
</kbd>
<br><br>

8. In the **Edit** drop-down list, select **Forms**.
9. For each of the forms listed, in the **Not Deployed** drop-down list, click **Enable for Web Service**. 
Note: Forms may already be deployed to Web Service and this step may not be necessary.

<kbd>
    <img src="/media/enable_ws.png" width="300">
</kbd>
<br>

<kbd>
    <img src="/media/form-ws-all.png" width="500">
</kbd>
<br><br>


10. After you Enable each form for Web Service, the drop-down list label will change to **Web Service**.
11. For the form named __Rollbar Alert__, in the **Web Service** drop-down list, click **Sender Permissions**.
12. Add the **API_User** you created above, and then click **Save Changes**.

<kbd>
    <img src="/media/sender_permissions.png" width="300">
</kbd>

<br><br>

## Get the xMatters Inbound Integration Endpoint URL

1. In the **Edit** drop down list on the __Rollbar Communication Plan__ Click **Flow**.
2. Click on the __Rollbar Alert__ Flow.

<kbd>
    <img src="/media/access_flow.png">
</kbd>
<br><br>

3. On the Flow Canvas, Double Click on the step named **Rollbar Flow Trigger**. This is the inbound http trigger for the Flow.

<kbd>
    <img src="/media/rollbar-trigger.png">
</kbd>
<br>
<kbd>
    <img src="/media/inbound-flow.png">
</kbd>
<br><br>

4. Change the _Authenticating User_ to the **API_User**

You must supervise this user and it must have a Web Service User Role. If you cannot select the **API_User** it is because you do not supervise that user, or they do not have the REST Web Service User role. When you create a new user, you are automatically set as that users' supervisor. If you do not see the user that you created, most likely the REST Web Service role is missing.

5. Copy the URL listed under the **Trigger** section.

You will need this URL for configuring Rollbar.

  <kbd>
    <img src="/media/trigger_url.png">
  </kbd>

<br><br>

## Customize your xMatters Flow

You can customize this integration by adding additional Flow Steps to post to chat ops tools, create tickets or anything else you can dream of.

_Here is an example of a customized Flow that posts to chat tool and creates a ticket:_

<kbd>
<img src="/media/customize-steps.png">
</kbd>

## Customize Rollbar Flow Trigger Step

1. In the Triggers tab under HTTP Requests section, click the Cog beside Rollbar HTTP Request and then Edit.

<kbd>
    <img src="/media/edit_trigger.png">
</kbd>
<br><br>

2. Go to the **OUTPUTS** Tab and add new **Step Outputs**. Outputs are values that will be available for subsequent steps.

<kbd>
    <img src="/media/create_outputs.png" width="550px">
</kbd>
<br><br>

**Note:** The Rollbar webhook format is predefined and most values are already part of this integration with the exception of **custom data**. Custom elements can be defined when sending an item to Rollbar. The custom data will be included in the payload to xMatters. You will need to add Outputs to the xMatters Inbound HTTP Request for Rollbar Step.
This is one of the methods that you can use to send custom recipient data to xMatters.

For information on setting Rollbar custom parameter go here: https://docs.rollbar.com/reference#getting-started-1

'''
    // Optional: custom
    // Any arbitrary metadata you want to send. "custom" itself should be an object.
    "custom": {
        "recipient": "xMatters Group",
        "your custom data" : "Custom Value"
        },
'''

The integration already looks for custom.recipient values. It will take any value here and add it to a recipient object and notify them with the xMatters alert. You do not need to include this value and can add your own as desired.

3. Go to the **SCRIPT** tab and modify your script appropriately.

- Each Output added in Step 2 will need to be mapped to a custom value in your payload. This takes the incoming value from Rollbar payload and sets the xMatters properties to hold these values.

<kbd>
    <img src="/media/custom-values.png" width="650px">
</kbd>
<br><br>

__Where__:

    __output['customValue01']__ - this is an output added in step 2. The output name is "New Output"
    __var_occurrence.body.custom.Custom_Parameter01__ - this is a value in your payload with the key "Custom_Parameter01" sent to xMatters from Rollbar.



## Add additional / custom properties to the Rollbar Alert Form.

1. Exit Flow Designer.

2. Navigate to the Forms section of Rollbar Communication Plan.

3. Beside Rollbar Alert Form, click **Edit** and go to **Layout**.

<kbd>
    <img src="/media/rollbar_alert_form.png">
</kbd>
<br><br>

4. Create new Properties.

<kbd>
    <img src="/media/add_property.png">
</kbd>

5. Drag new Properties onto the Form.

6. Save Changes.

7. Make any required changes to **Messages** and **Responses**.

<kbd>
    <img src="/media/messages_responses.png" width="350px">
</kbd>

<br><br>

## Customize **xMatters Create Event (Rollbar Alert)** Step

Once you have added new properties to the Rollbar Alert form, they will become available in the **xMatters Create Event (Rollbar Alert)** Step for you to map payload properties to.

1. On the Flow Canvas double click the **xMatters Create Event (Rollbar Alert)** Step

<kbd>
    <img src="/media/create_event_step.png">
</kbd>
<br><br>

2. Drag items from the right to the appropriate fields on the left. Any new fields you have added to the form layout will be available here.

<kbd>
    <img src="/media/custom_create_event.png" width="650px">
</kbd>
<br><br>

## Set xMatters Constants

1. Go to Rollbar communication plan click __Edit__ and go to __Integration Builder__. 

2. Click __Edit Constants__.

3. Set each of the following constants. 

- __Rollbar Account Read__ - [How to Get Rollbar Account Access Tokens](https://docs.rollbar.com/reference#section-account-access-tokens)
- __Rollbar Read__ - [How to Get Rollbar Project Access Tokens](https://docs.rollbar.com/reference#section-project-access-tokens)
- __Rollbar Write__ - [How to Get Rollbar Project Access Tokens](https://docs.rollbar.com/reference#section-project-access-tokens)
- __RQL Query String 01__ - Write your own [RQL Query](https://docs.rollbar.com/docs/rql) and put it here. This can be ran from an xMatters response option. 

<kbd>
    <img src="/media/constants.png" width="650px">
</kbd>
<br><br>

See [How to Get Rollbar Access Tokens](#get-rollbar-access-tokens)



# Configuring Rollbar

## Get Rollbar Access Tokens 

__To access your Rollbar tokens, navigate Rollbar menus as follows__:

- __Account Access Tokens__: Click User Name -> Account Settings -> Account Access Tokens.
[How to Get Rolbar Account Access Tokens](https://docs.rollbar.com/reference#section-account-access-tokens)

    <kbd>
        <img src="/media/account.png" width="100px">
    </kbd>
    <kbd>
        <img src="/media/aat.png" width="1000px">
    </kbd>
    <br><br>

- __Project Access Tokens__: Settings -> Project Access Tokens.
[How to Get Rolbar Project Access Tokens](https://docs.rollbar.com/reference#section-project-access-tokens)
    <kbd>
        <img src="/media/settings.png" width="1000px">
    </kbd>
    <kbd>
        <img src="/media/pat.png" width="1000px">
    </kbd>
    <br><br>


## Create a New Notification Webhook

Follow instructions here to create new Notification Webhook:<br>
https://docs.rollbar.com/docs/webhooks

This integration will work with the following templates but can also work with whatever you desire.:

- 10^th Occurrence
- High Occurrence Rate
- New Item
- Every Occurrence
- Item Reactivated
- Item Reopened
- Item Resolved

You should create separate rules for each event you want to send xMatters. A separate rule is usually used if you want to target different recipients and include the recipient as a webhook URL parameter.

Here is how you should configure your new Webhook rule:

'''
**Webhook URL**: 
Set this to the xMatters Inbound Integration Endpoint URL.
[Get the xMatters Inbound Integration Endpoint URL here](#get-the-xmatters-inbound-integration-endpoint-url)

You can specify recipients and other parameters by adding url parameters at the end of the integration URL.
For instructions on how to do this see:
[Add URL Parameters to the Rollbar Notification Webhook](#add-url-parameters-to-the-rollbar-notification-webhook)

**Format**:
JSON

**Filter**: 
As desired
'''

<kbd>
    <img src="/media/settings.png" width="75px">
</kbd>
<br>
<kbd>
    <img src="/media/notifications.png" width="125px">
</kbd>
<br>
<kbd>
    <img src="/media/webhooks.png" width="500px">
</kbd>
<br><br>


## Set xMatters Recipients in Rollbar

There are two ways to target xMatters Users and Groups from this integration.

1. Set Custom Data on your Rollbar item.
2. Add URL Parameters to the Rollbar Notification Webhook.


You can use either one or both of these methods. You must use at least one method, or your integration will not target anyone and will fail.

### Set Custom Data on your Rollbar item.

See Rollbar documentation for Getting Started / Create Item:
[https://docs.rollbar.com/reference#getting-started-1](https://docs.rollbar.com/reference#getting-started-1)

When creating an item, you can add custom values to the data element. Here is an example below.

'''
{
	"access_token": "c16d776575df",

	"data" :{
                 "environment": "development",
				 "level": "Warning",
				 "title": "My custom title",
				 "integrations_data" : {"id01": "data v1","id02": "data v2"},
				 "filename" : "export.jst",
				 "context": "Main application core function",
				 "method": "post-method",
				 "framework": "python",
				 "path": "https://xmapi.com",
				 "body": { "message": {"body": "Many new parameters and data values"} },
				 "custom": {"recipients":"Admin Group"}
             }
}
'''

The integration is configured to look for the recipients custom element and will add any users / groups listed here as recipients in the xMatters event.

For more information on adding custom data go here: <br>
[https://docs.rollbar.com/reference#getting-started-1](https://docs.rollbar.com/reference#getting-started-1)

### Add URL Parameters to the Rollbar Notification Webhook

You can specify recipients and other parameters by adding URL parameters at the end of the destination webhook URL. See [Create a New Notification Webhook](#create-a-new-notifiation-webhook)

This integration is specifically configured to look for a URL parameter **"recipients"** and add specified recipients to the xMatters alert.

This will help you customize the target xMatters groups / users from the Destination URL and make targeting appropriate people easier. You could create multiple Webhook Rules targeting different groups / users in xMatters.

- You can specify xMatters **Groups** as well as **Users**.
- Specify more than one by separating with a comma.
- Add the recipients URL parameter to the end of the inbound integration URL.

**Examples**:

- **Target a single group**<br>
  _&recipients=Database_

- **Target a single user**<br>
  _&recipients=jsmith_

- **Target a group and a user.** Notice each value is comma separated.<br>
  _&recipients=Database,jsmith_

- **To target a recipient with a space in the name.** You must URL encode the space.<br>
  _&recipients=Cloud**%20**Devops_

  _%20_ is the URL encoded value for a space. If you have other special characters, they could cause a problem and should be encoded.

  Here is a character encoded to assist you:
  https://meyerweb.com/eric/tools/dencoder/

**Full Example URL**:<br>
https://company.cs1.xmatters.com/api/integration/1/functions/769bc32d-07bc-4a720/triggers?apiKey=b6d5-3f1bd65ae91d&recipients=Cloud%20Devops

**Other Notes**:<br>

- Make sure to include the **&** before recipient or any other parameter you decide to add.

- If you want to add additional parameters, you can do so by adding **&parameter=value**<br>
  This is an easy way to add parameters like severity so xMatters can take different workflows for different values.

- If you add additional parameters you will need to also follow instructions here [Customize Rollbar Flow Trigger Step](#customize-rollbar-flow-trigger-step)

# Troubleshooting

Trigger a new Lightstep Alert and check that it makes its way into xMatters.

You can check the Activity Log of Flow Designer with these instructions.
https://help.xmatters.com/ondemand/xmodwelcome/flowdesigner/activity-panel.htm
