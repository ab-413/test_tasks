Besides doing devops stuff for ourselves and for clients, we also do support and development of open-source modules.

One of such projects is the development of terraform modules for Google Cloud.

As a test task, you need to create such a terraform module and write automated tests for it.

Take a look at some other terraform modules from «terraform-google-modules» organization on github.

You need to write a similar terraform module for running «redis» in Google Cloud. It needs to be a VM with redis installed, not the cloud google redis service.

Requirements
Generate a new terraform module using this template generator.
Push it to your own personal github as PRIVATE repo (github allows private repos on personal accounts for free). When you are done with the test task, you’ll just add one of our reviewers as a collaborator.
The terraform module has to have only 1 configurable parameter —  «port» which redis is going to run on.
It has to provision a VM on any OS you would like (for example, on debian).
Make startup script which will install and run the redis on VM (hint: you would probably need to use metadata_startup_script or metadata.startup-script or metadata.user-data field to execute this script)
Write tests.
Read CONTRIBUTORS.md in your project. It has information about running tests in the test/ folder.
IMPORTANT:
- In order to create a global service account and provide a folder-access to it, you must have a G-Suite and have an Organization in Google Cloud. G-Suite has a free trial period. If you don’t have that available to you for some reason, you can ask me for access to one of our Organizations (razer_ua on skype).

- Here is more information about Folders.

- After you have created an Organization on Google Cloud using G-Suite, to create a global service-account with access to folders, use the following script. 

The tests are written mostly in InSpec. You would need to replace those dummy InSpec tests with the ones which will test your new redis module.
To understand what the InSpec is and why you use it, please watch the following video.
Your tests must check for at least the following 3 things:
- The VM is created and running.

- The custom redis port (which can be specified in the module options) is open (the decision on whether to open it to the global internet or to some particular network is up to you).

- And that redis is actually running on this port.

Send us a github link once you’re done and let us know how much time we should pay you for. We will pay you for the work done (up to 20 hours) at your monthly rate prorated by the number of hours it takes you as long as you have met the requirements and you join us to work full-time. We will use the quality of your deliverable along with the time it took you to do the task to evaluate you. If everything looks good, we will hire you.
Additional Information
Once you get the tests working (following the CONTRIBUTING.md guide), if you want to poke around your new project, which was created when you ran the tests, you can assign yourself project editor role. To do this, login under your service account (using its credentials.json):

gcloud auth activate-service-account --key-file credentials.json.

And execute the following command (remember that you must be logged in under service account credentials):

gcloud projects add-iam-policy-binding <new project> --member=user:<username>@<organization> --role=roles/editor.

It should not be general practice to assign yourself project editor, but when debugging the Project Factory module, it may be helpful. Similarly, you may remove these permissions when you are done by issuing the following command:

sgcloud projects remove-iam-policy-binding <new project> --member=user:<username>@<organization> --role=roles/editor.