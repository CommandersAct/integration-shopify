# ![TagCo logo](/Screenshots/tag.png) Shopify Integration
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
* It is **highly recommended** to use a Shopify **Plus** account. The integration is still possible with the basic Shopify account; however, the checkout steps won't be tracked and some custom code will have to be injected on the Thank You page if you want to be able to track conversion. With the Shopify Plus account you won't need anything else.
* Your TagCommander account ID, if you don't know it, you can find it directly in the address bar of your browser when you're navigating in your TagCommander account:

  ![TagCo screenshot](/Screenshots/TagCo_Account_ID.png)
* Your TagCommander container's filename, if you don't know it, you can find it in here:

  ![TagCo_filename_path](/Screenshots/TagCo_filename_path.png)
  
  ![TagCo_filename](/Screenshots/containers_file_name.png)
## Steps
1. Adding the settings panel. You need to navigate to Config/settings_schema.json and open it in the editor:

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
2. Adding the container
3. Adding the datalayer
4. Including the setup on the pages
5. Including the setup in the checkout tunnel
