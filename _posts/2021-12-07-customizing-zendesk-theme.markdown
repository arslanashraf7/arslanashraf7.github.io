---
layout: post
title:  "Customizing Zendesk Theme"
date:   2021-12-07 03:53:01 +0500
categories: jekyll update
---
You might have been in a situation where you wanted to customize your Zendesk Help Center but you were not fully able to do that using the built-in customizations mentioned in [Customizing your help center theme](https://support.zendesk.com/hc/en-us/articles/4408839332250-Customizing-your-help-center-theme)

I'm going to provide a list of stemps that you can follow to customize your own zendesk themes.

- Clone the Zendesk's `Copenhagen` theme [repository](https://github.com/zendesk/copenhagen_theme) (This repository contain all the basic structure needed for the theme)
- Setup a trial instance
    - Create a trial account on [Zendesk](https://www.zendesk.com/)
    - Create a Sandbox on existing Zendesk account following [this link](https://support.zendesk.com/hc/en-us/articles/4408828617370-Testing-changes-in-your-standard-sandbox)
    - Make sure to opt. In for `Zendesk Guide` integration once you’ve created an account (This step might require you to confirm through email again)
- After the setup and account confirmations go to [Admin Settings](https://<YOUR_ZENDESK_DOMAIN>/agent/admin/api/settings) (`Admin->APIs-> Generate Token`) and generate an API token that you’ll need to publish local theme changes on you Zendesk domain.
- Go to [Workbench](https://<YOUR_ZENDESK_DOMAIN>/theming/workbench) and check your theme (By default it should be a Copenhagen theme)
- Enable Help Center for your account by visiting [General Settings](https://<YOUR_ZENDESK_DOMAIN>/hc/admin/general_settings)

{% highlight ruby %}
Running the theme locally
 
1- Create a .zat file in your local theme directory (It should look like below)
  {
      "subdomain": "<YOUR_ZENDESK_SUBDOMAIN>",
      "username": "<ACCOUNT_EMAIL>/token",
      "password": “<GENERATED_TOKEN>”,
      "zat_latest": "3.8.1",
      "zat_update_check": "2021-02-16"
  }
{% endhighlight %}

Follow this link to install ZAT https://support.zendesk.com/hc/en-us/articles/4408822095642

- To install packages yarn install
- To build Css/style files & assets ./bin/compile.rb
- To run your theme preview zat theme preview (This is temporary deployment and will end once your local zat server stops)
- To create an uploadable bundle

{% highlight ruby %}
Cd ..
zip -vr <ZIP_FILE_NAME>.zip <YOUR_THEME_DIRECTORY> -x "*/node_modules/*"
To upload a permanent them, Go to https://<YOUR_ZENDESK_DOMAIN>/theming/workbench and upload your created .zip file & click public in the menu
{% endhighlight %}

**General Representations**

I’ll add a couple of examples about the content of the theme and how to change that

- For all the frontend related changes you’d find HandleBar files(`*.hbs`) in `/templates` directory and (`_*.scss`) files in `/styles` directory e.g. if you’d want to change things in footer you’ll have to change the contents of (`footer.hbs & _footer.scss`) respectively

- For adding new type of `settings/variables` you need to make changes in (`manifest.json` - For adding a new key/value) and (en-us.json - For adding a description of how it's presented on the Zendesk admin panel)

- For adding new assets and using them through settings you will add th assets file in `<THEME_DIR/settings>`
