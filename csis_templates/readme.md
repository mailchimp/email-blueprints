CSIS: Training and Documentation
================================

### Credentials & SF Connection for Stage & Dev Sites
**Stage:** http://forumone:f1dev@stage.csis.byf1.io/
-Connects to **ThinkShout** sandbox: https://cs43.salesforce.com
-Credentials are managed separately by individuals
**Dev:** http://forumone:f1dev@dev.csis.byf1.io/
-Connects to **ThinkShout** sandbox: https://cs43.salesforce.com
-Credentials are managed separately by individuals

### Email Subscription & Management
CSIS user profile data (synched between Salesforce and RedHen) is automatically synched with MailChimp in the following fields:
-First Name
-Last Name
-Default Email
-CSIS All Subscription
  *Topical Interests
  *Regional Interests
-Member list Subscription
-Press list Subscription
-Unique ID (used for updating subscriptions on the csis.org website

Users who log in to the site can manage their public subscription preferences on their user profile page (/user or /user/ID/edit).

Anonymous site users can sign up and manage these subscription preferences on the CSIS email subscription page (/subscribe). CSIS administrators can change these preferences on behalf of CSIS users within the RedHen contact profile (/redhen/contact) or directly from Salesforce and MailChimp.

Mailchimp Administrative settings can be managed at Configuration>Web Services>MailChimp

**Subscribe Form** is the configuration page for updating the content displayed on the CSIS email subscription page (/subscribe).

**Campaigns** is for creating MailChimp campaigns based on Drupal site content (Events and Publications).

How to add public email subscriptions preference links to "CSIS All" campaign emails - related document: [CSIS MailChimp - Creating subscription management links for Public list templates](https://docs.google.com/document/d/1rUwr8D8v8ErZgZ3yKDIVWZNhyntnQ9a3hXREQlDzC2E/edit?usp=sharing)

##### Topics and Regions
In order to change the topic and regions in Drupal and Salesforce, there are a few steps that need to be followed in order:
1. Go to the filds for the Redhen Contacts: https://new.csis.org/admin/structure/redhen/contact_types/manage/general/fields
2. Select either the Topical or Regional list field
3. The list of items will be in the field
4. If a value needs to be changed, you have to create a new value below the item you want to change.
5. Switch to Salesforce and move any contacts to this new value from the old value.
6. Manually trigger the updated date for all contacts with this change.
7. Run cron on Drupal to pull the new values for that contact.
8. The old value can then be deleted.

###### Reordering of Topics
The topic list canbe reordered at any tie and this will be represented in the user view of these.
###### Topic Headers
Topic headers get some additional formatting by specific code and will need to be identified and changed in code if changes are necessary. The order of these topics in the list doesn't directly affect whrere they appear in the list as well.

##### MailChimp - Creating subscription management links for Public list templates
In compliance with the CAN-SPAM act of 2003, every mass email sent to CSIS contacts must include an “unsubscribe” link. To reduce usage of this link, every email should also include a “update your preferences” link to allow individuals to tweak their email preferences rather than unsubscribing.

MailChimp provides both of these links, by default, in their custom email templates. If you are editing, or creating, a custom email template, you must ensure that both these links are present. 

### Event & Publications MailChimp Campaigns
Events and publications created on csis.org can be sent directly to MailChimp as campaigns to ensure campaings are consistently formatted and to speed the creation and formatting of these prior to being sent to subscribers. The following steps detail how to send an existing event or publication to MailChimp as a campaign and the templates used to format them. 
##### Events
1. Create the CSIS event as you normally would following the directions below (Events & Registrations > Creating Events)
2. Once a draft or published version is complete, select the "Add to Campaign" button.
3. Configure campaign settings, including seecting the "Event Invite" template
4. The "Event Invite" template includes the necessary text from the event you are adding
5. The body of campaign email will be formatted based on a template in the code base called “node--email-content--event.tpl.php”. This template has been preformatted to include values from the event if values existed for them. The HTML for this can be modified after being sent to MailChimp or if needed to be done universally for the template can be done in code by ThinkShout. See GoogleDoc for code (Updated as of 1/11/2017)
6. To send the event to MailChimp as a campaign, Select the "Save as draft" button at the bottom
7. Once a campaign has been sent to MailChimp by selecting the "Save as draft" button, you must update the campaign content in MailChimp or select "Save as draft" to create a new campaign in MailChimp with the updated content.

##### Publications
The steps to create and send a Publication to MailChimp as a campaign is exactly the same as for Events, except that the template required in steps 3 and 4 should be “Publication”. This template is a different file in code (node--email-content--publication.tpl.php) and uses a different set of HTML to render in MailChimp. See GoogleDoc for code (Updated as of 1/11/2017)

### Events & Registrations
The CSIS site has three distinct registration “types”. Each has unique behaviors, but all share the same basic structure and administration options. We describe them from simplest to most complex.

##### Creating Events
To create a new Event, a user with the "Content Editor" role can log in to the Drupal site and use the "Content" menu selecting "Add content" > "Event"

There are a number of content fields that must be filled out, and a significant additional number that are optional. Optional fields can be populated later by returning to the event and editing it.

The type of event, and the associated registration behaviors, are controlled by the “Registration Type” field. It has a drop-down with the three types of CSIS Event. It is important to select the correct value the first time: changing the Registration Type after publication of the event on the live site is not recommended and may produce unexpected results.

Once you have saved your event, it will immediately create a corresponding Campaign object on Salesforce.

##### Managing Registrations and Attendance
Once you have created your event and received some registrations, you can manage those registrations by visiting the event page: click the "Manage Registrations" buttons, located below the title.

This will display a list of registrations for the event. (Note that you can do some sophisticated reporting on these registrations through Salesforce, but making changes should be done through Drupal: the changes will be reflected in Salesforce). You can view, edit, or delete the individual registrations using the links on the right column of the table.

If you are doing event check-in, you can rapidly set registration statuses by using the “Check-in” option on the top right.

This presents a display of all the existing registrants and a button to quickly check-in any of them. The search area on the top left can be used to quickly search all registrations by name or email address. The “check-in” button sets the registration to the “Attended” state. The “State” drop-down allows you to see the registration’s current state, as well as to set the state to any other options.

If you need to check someone in who did not register, you can do that using the “New Registrant Check-in” button above the Search tool. This will create a new registration for the event and immediately set that registration to the “Attended” state.

##### Managing Registration Behaviors

After an event has been created, some of the registration behaviors can be customized. If you are logged in as a Content Editor user, you can visit the event page and click “Manage Registrations”. From here, you will see a list of registrants with buttons above and to the right. From those buttons, select “Settings”

From this page, you can configure the following behaviors:
1. Enable/Disable Registrations:
    *Uncheck the "Enable" box to disable registrations
    *Use the "Scheduling" section to make registrations automatically enable/disable based on a date and time.
2. Set a capactiy limit for the event using the "Capacity" field. The default is 0, meaning there is no limit to the number of registrants.
3. Send an automated reminder email to registrants using the "Reminder" tool.
4. Change the message that appears after a registration has been completed, using the "Confirmation Message" option. Leave blank to display no message.
5. Set a “Confirmation Page”. By default, this is blank, meaning a registrant will remain on the Event page after completing registration. To send them to another site on the page, simply enter the path to that page. You can redirect them to any page on the site. Be sure to start the text with a “/”.

Note that there are fields for "Allow Multiple Registrations", "Spaces Allowed", and others. These fields *should **not** be altered.* Doing so may cause unpredictable behaviors and errors with the synchronization to Salesforce. Touch only the fields mentioned in items 1-5 above.

### Public Events
Public Events are listed on the events page (/events) for everyone visiting the site to see, even anonymous users (those who are not logged in).

Anyone viewing a Public Event can register for that event by clicking the “Registration” button, entering their registration details, and selecting “Confirm Registration”. After registering, the user will see a confirmation message at the top of the page, and can click “Registration” again to register another person if desired. They will also receive a confirmation email.

The email address entered is used to identify or create a corresponding Redhen Contact record, which is then given a “Registration” for the event. If someone enters an email address for a registration that has already been used to register for that event, they will receive an error message indicating that the person is already registered.

### Private Events
When a Content Editor is creating or updating a Private Event, they will see an additional field at the bottom of the form after selecting the “Private Event” registration type. This field is called “Invitees”.

Only the people added to this invitees list will be allowed to see this event and register for it. You can invite people by beginning to type their name or email address into a blank invitee field: the system will auto-complete and allow you to select a Redhen Contact matching what you have typed in. (If the person you wish to invite does not appear, you must go to the Redhen menu and create a Contact for that person.)

Use the “Add another item” button to invite additional people -- you may only add one per line.

##### Registration
In order to see a Private Event, the invitee must log in to your site with an email address that matches the email address on the Redhen Contact you selected in the “invitees”. If they do not already have an account, they can create a new User on your site with that email in order to do this.

Anyone who is logged in and invited to a Private Event can see it on the events page, and can register for that event by clicking the “Registration” button, entering their registration details, and selecting “Confirm Registration”. After registering, the user will see a confirmation message at the top of the page, and will also receive a confirmation email.

Anyone who is not invited to the event, or is not logged in, should not see the event on the Events Page.

Once a user has registered for the event, if they return to the event page later, they will see the “Registration” button has been replaced by a “Manage Registration” button. This button allows them to update their registration details or cancel their registration.

### Conference Events
Conference Events are initially very similar to Public Events: they require similar fields to be populated and they are visible to all site visitors. However, there are two major differences:
1. Users must login to the site in order to register for Conferences (they can't just type in their email address to the registration form)
2. Conferences can have a collection of Sessions attached to them, which are like mini-events that have their own registrations. Sessions are covered in the next section.

##### Registration
When viewing a Conference Event, an “anonymous” user (who is not logged in) clicking the “Registration” button will be prompted to login or create an account. Once they have logged in, they can press the “Registration” button again, but this time they will see a form allowing them to Register.

Once a user has registered for the event, if they return to the event page later, they will see the “Registration” button has been replaced by a “Manage Registration” button. This button allows them to update their registration details or cancel their registration.

### Event Sessions
Sessions are a special type of event that are attached to Conferences. From the perspective of the registrant, this provides the ability to register for an Event, and the associated sessions, at the same time: they may not be aware that it is treated as its own Event by the underlying systems, and that’s OK.

From the perspective of a CSIS Content Editor, though, it helps to understand that these sessions are actually mini-events with their own registrations.

##### Creating Sessions
There are two ways for Content Editors to create Sessions. The same way other types of content can be created, you can go to the Content menu, select Add Content, and choose “Event Session”. However, this is not the recommended way to create Sessions! The recommended technique is to start by going to the Conference Event that the Session will be a part of and clicking the “Sessions” tab on the right side below the title.

This will present a listing of current sessions for this Conference, and an “Add Session” button. Clicking this button will create a new Event Session with some default values set based on the Conference.

Complete all the required fields, and pay special attention to the start and end date and time. The listing of Sessions that will appear on Conferences needs these to match exactly for parallel sessions to be displayed correctly.

Once you save your session, it will appear on the Registration form for the Conference event, along with all the other sessions for the event, with a checkbox next to it. Registrants can now use these checkboxes to register for the individual Sessions.

For Sessions that have perfectly overlapping times, they will be displayed in the same timing area, and registrants will only be able to select up to one checkbox form each area.

Note that everything in “Managing Registration Behaviors”, above, applies to sessions as well. You can load the individual sessions from the Conference “Sessions” listing: simply click the Session’s name. From there, you will see the familiar “Manage Registrations” button, and you can also edit your Session.

### Donations
##### Creating and Configuring Donation Pages
When you are logged in as a Content Editor, any basic “Page” content type on your site can be turned into a Donation Page by selection “Donation” under “Donation Type” at the bottom of the Page edit form.

This setting will enable a single-page donation form at the bottom of the page’s content.

Generally, you will only want to manipulate the existing “Donation” page. To do so, visit the page as a Content Editor and look for the “Donations” tab.

Clicking “Donations” will take you to a list of Donations that have been made using this page. On the top right you will see a “Settings” button.

Click this button to configure the behavior of your donation page using the following fields:
-“Enable” -- Uncheck this button to make the donation form disappear until the button is re-checked.
-“Scheduling” -- Use dates and times to automatically trigger enable/disable on this donation page.
-“Confirmation Page” -- Enter the path to another page on the site to redirect anyone completing the donation form to a specific page. Otherwise, they will remain on the Donation page. Note: only enter the part of the URL after the -“Domain”, so if you want to send them to “http://www.csis.org/donate/thank-you”, you would enter “/donate/thank-you” here.
-“Confirmation Message” -- This message will display on the page after the donation is completed. You can use “Tokens” to customize the message for each donation by entering the values described in “Available Tokens”.
-“Donation Entry” -- Change the way people enter donation amounts. It is not recommended that you change this value. Doing so will alter the appearance of the donation amount form element.
-“Amount Selection Label” -- Change the text that displays above the amount selection.
-“Donation Amounts” -- The amount selection list. Each item on the list should be on its own line, in the format “Amount|Label”. Note that this is dangerous, as you can easily create Labels that do not match the Amounts! Take care when editing this field.
-“Other Option Label” -- Label for the “Other” amount option.
-“Minimum/Maximum Donation” -- Prevent donations outside these ranges. Blank for no restrictions.
-“Submit Button” -- the text to display on the donation submission button.

##### Processing Donations
Any user visiting the page may complete the form to make a donation. If the user is Anonymous, the email address they enter will be used to attach this donation to any existing Contact in your system with the same email address. If the email address is not present in your system, it will create a new contact to attach to using the form values.

If the user chooses a “Recurring Donation”, a Recurring Order is created on the Drupal site, which will automatically process new donations for the contact on a monthly basis.

Single Payment
    -As a User
    -As an Admin on Drupal
    -Expected SF Behavior or related fields in SF
    
Recurrent Payment
    -As a User
    -As an Admin on Drupal
    -Expected SF Behavior or related fields in SF
    
##### Please see the [GoogleDoc](https://docs.google.com/document/d/12mbJ8rJs2_U0rtDp3s3ZyhknKm6D83exDTYDGDBx3tk/edit#) for more detailed information.
