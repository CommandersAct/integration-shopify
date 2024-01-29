[![Commanders Act Logo](/Screenshots/CommandersAct.png)](https://www.commandersact.com/)
# Shopify Integration
## Overview
Welcome to TagCommander, the Commanders Act TMS solution, we are glad to help you to add it to your Shopify based e-commerce, easily and in a time-effective fashion.
This procedure will achieve the following:
* creation of the TagCommander Datalayer
* integration of the TagCommander container
## Time necessary to complete this installation
It should be feasible in between 5 minutes and 1/2 hour depending on the user's experience with Shopify and TagCommander. This tutorial does not assume previous technical knowledge, though a general understanding of Shopify and TagCommander is recommended.
## Structure of this repository
The folders which are relevant for the installation are Config and Snippets, you can ignore the rest
## Prerequisites
* A TagCommander Account with CDN enabled, if you don't have one, please reach out to Commanders Act, the contacts are on this page: https://www.commandersact.com/en/contact/
* This setup has been designed for a **CDN connector provided by Commanders Act**, if you don't have one or aren't sure, please contact Commanders Act
* This setup allows only **one container** to be added to the site, should you need more, please contact your dedicated Commanders Act consultant
* It is recommended to use a Shopify **Plus** account. The integration is still possible with the basic Shopify account; however, the checkout steps won't be tracked and some custom code will have to be injected on the Thank You page if you want to be able to track conversion. With the Shopify Plus account you won't need anything else.
* Your TagCommander account ID, if you don't know it, you can find it directly in the address bar of your browser when you're navigating in your TagCommander account:

  ![TagCo screenshot](/Screenshots/TagCo_Account_ID.png)
* Your TagCommander container's filename, if you don't know it, you can find it in here:

  ![TagCo_filename_path](/Screenshots/TagCo_filename_path.png)
  
  ![TagCo_filename](/Screenshots/containers_file_name.png)
## Steps
### 1. Adding the settings panel. 
You need to navigate to Config/settings_schema.json and open it in the editor. To do that follow Online Store -> Themes -> Actions -> Edit code as shown below:

![Shopify_path_editcode](/Screenshots/Shopify_path_editcode.png)

At this point, scroll down the code folders to locate the Config folder (1), locate the settings_schema.json file and edit it by double clicking on it.
In the editor, **locate the last closing curly bracket** (3). 

![Shopify_locate_closing_curly](/Screenshots/Shopify_locate_closing_curly.png)

At this point, add a comma after the closing curly bracket, copy the code below and pste it into the editor:

  ```javascript
	
  {
    "name": "Commanders Act",
    "settings": [
      {
        "type": "text",
        "id": "ca_account_id",
        "label": "Commanders Act Account ID",
        "info": "If you don't know it, contact your Commanders Act Consultant"
      },
      {
        "type": "text",
        "id": "ca_container_filename",
        "label": "Container's filename",
        "info": "Check your Tag Commander interface or contact a Commanders Act Consultant"
      },
      {
        "type": "radio",
        "id": "ca_environment",
        "label": "Environment",
        "options": [
          {
            "value": "\/uat",
            "label": "UAT"
          },
          {
            "value": "",
            "label": "Production"
          }
        ],
        "default": "\/uat",
        "info": "Commanders Act environment, see the deploy tab in the TagCommander interface"
      },
      {
        "type": "checkbox",
        "id": "ca_tagco_enabled",
        "label": "Enable",
        "default": false,
        "info": "Check to enable CommandersAct"
      }
    ]
  }
  ```
This code can also be found, if you prefer, in the config folder of this repository, in the file setting_schema_PARTIAL.json. 

This is what the editor should now look like, with the added code (1) . Now you can save the file (2):

![Shopify_config_json_paste](/Screenshots/Shopify_config_json_paste.png)

Congratulations ! You have now installed the config panel for your TagCommander Shopify Installation. 

### 2. Configuring the module
Go to the configuration panel which has been created with the step 1. You can do that via Online Store -> Themes -> Customize

![Shopify_path_to_config_panel_1](/Screenshots/Shopify_path_to_config_panel_1.png)

You'll see a new entry in the Theme settings menu:

![Shopify_path_to_config_panel_2](/Screenshots/Shopify_path_to_config_panel_2.png)

Click on it and you'll get to the actual Commanders Act configuration panel:

![Shopify_config_panel](/Screenshots/Shopify_config_panel.png)

here you will enter the TagCommander (Commanders Act) account ID and the container's filename, as explained in the Prerequisites section.
Environment is normally UAT for your test environment, if you have one, Production otherwise. This will reflect the two deployment connectors which you normally should have configured in TagCommander:

![UAT_prod_TagCo](/Screenshots/UAT_prod_TagCo.png)

### 3. Adding the container
1. Navigate this repository to Snippets/tagco.liquid 
2. Copy the content of the file into the clipboard (Ctrl-C in Windows).
3. Go back to the Theme Code edit section, as you did in Step 1. 
4. Scroll to Snippets -> Add a new snippet and create a snippet with exactly the same filename as the file  in the repository, i.e. "tagco.liquid" 
	![Shopify_add_new_snippet](/Screenshots/Shopify_add_new_snippet.png)
5. Paste the code in the editor (Ctrl-V in Windows) and save
	![Shopify_save_template](/Screenshots/Shopify_save_template.png)
	
### 4. Adding the datalayer
Create a new snippets, much the same way as you did in "Adding the container" step, using the content of this repository's file Snippets/dl_ca.liquid . Remember to use the exact same filename "dl_ca.liquid"
### 5a. Including the setup on the pages and checkout tunnel - Shopify **Plus**
Go back to the Theme Code edit section, as you did in Step 1.
1. Scroll to Layout. You'll see the layout files. Typically you'll have theme.liquid and checkout.liquid 
2. Copy the following two lines into the clipboard

	```twig
		<!-- inclusion of TagCommander -->
		{% include 'tagco' %}  
	```
3. Paste the code in the theme.liquid and checkout.liquid templates, just above the closing ```</body>``` tag and save the layout:

	![Shopify_add_inclusion_in_layout](/Screenshots/Shopify_add_inclusion_in_layout.png)

### 5b. Including the setup on the checkout tunnel - Shopify **Basic**
Go back to the Theme Code edit section, as you did in Step 1.
1. Scroll to Layout. You'll see the layout files. Typically you'll have theme.liquid
2. Copy the following two lines into the clipboard

	```twig
		<!-- inclusion of TagCommander -->
		{% include 'tagco' %}  
	```
3. Paste the code in the theme.liquid template, just above the closing ```</body>``` tag and save the layout:

	![Shopify_add_inclusion_in_layout](/Screenshots/Shopify_add_inclusion_in_layout.png)
	
4. Go to Admin->Settings->Checkout as shown below
	
	![Shopify Basic Checkout Pers 1](/Screenshots/shopify_basic_checkout_pers_1.png)

5. In the Checkout section, scroll down to "Order Processing" and paste the code of the snippet dl_tagco_checkout_basic.liquid into the field "additional scripts" as shown below:

	![Shopify Basic Checkout Pers 2](/Screenshots/Shopify_basic_checkout_pers_2.png)
	
6. Manually edit the beginning of the code, in particular the lines:
	<!-- you need to enter your TagCommander account ID here -->
	{% assign ca_account_id = "0000" %} 		

	<!-- you need to enter your TagCommander container file name here -->
	{% assign ca_container_filename = ""%} 		

	<!-- enter exactly "\/uat" for UAT environment, leave empty for Prod -->
	{% assign ca_environment = "" %}			

	<!-- enter false to disable TagCommander -->
	{% assign ca_tagco_enabled = true %}	

7. Scroll down and save

### 6. QA the setup
**Congratulations ! You have installed TagCommander in your Shopify store !**
To perform a basic check on the setup, install the Commanders Act chrome extension if you don't have it already. Just search for it with any search engine.
1. Navigate to your site
2. open the Commanders Act widget and see the container and the active tags (if there are any):
	![site_ca_widget_demo](/Screenshots/site_ca_widget_demo.png)
3. Open the browsers console by hitting F12 or right-click and inspect anywhere on the screen
4. Make sure you're on the console tab
5. on the command line enter "tc_vars" ; this will visualize the datalayer :
	![site_console_dl_qa](/Screenshots/site_console_dl_qa.png)
		
## Licence
See the LICENCE file for details.
