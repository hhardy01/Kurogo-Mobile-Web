#################
Emergency Module
#################

The emergency module provides a mobile interface to a sites emergency information. 
The module can display the latest emergency information and a list of emergency contacts.
The data source for this module can come from a drupal server, running emergency drupal module
which can be found in the add-ons at *add-ons/drupal-modules/emergency*.  Alternatively,
a standard RSS feed can be used for the emergency notice, and the contacts list can be 
configured with an ini file.

=================================
Configuring the Server Connection
=================================

In order to use the emergency module, you must first setup the connection to your data.
At minimum you need to configure the RSS feed which gives the most recent emergency information,
by editing the `notice` section of *config/feeds/emergency.ini*.

* If you are using the add-on emergency drupal module, you can set the RSS_URL to
  "http://YOUR_DRUPAL_SERVER_DOMAIN/emergency-information-v1", where YOUR_DRUPAL_SERVER_DOMAIN.
  Otherwise just set the RSS_URL to the appropriate RSS feed.

If you also want to include emergency contact phone numbers, you will need to include
a `contacts` section in *config/feeds/emergency.ini*

**Configure Contacts List**

Configure contacts list to connect to the drupal emergency module:

* CONTROLLER_CLASS = "DrupalContactsListDataController"  
* DRUPAL_SERVER_URL = "http://YOUR_DRUPAL_SERVER_DOMAIN"  
* FEED_VERSION = 1

Otherwise you can configure the contacts list directly in this ini file with,
CONTROLLER_CLASS = "INIFileContactsListDataController", and you will need a
`primary` section for primary contacts and a `secondary` section for secondary contacts.
Each contact is formatted as follows::

  title[] = "Police"  
  subtitle[] = ""  
  phone[] = "6173332893"  

=======================================
Using Drupal Emergency Module
=======================================

**Installation**

Follow the standard procedure for installing a drupal module, which is:  

* In order to install this module you must first install the 
  drupal CCK (Content Creation Kit) module and the drupal Views module  

* copy *add-ons/drupal-modules/emergency* into the *sites/all/modules/* directory  

* In the drupal administration panel go to modules then select the "Emergency Info"
  module and click "save configurations". 

**Usage**

To input an emergency notification: create a node of content type "Emergency Notification",
the RSS feed will only show the most recently updated Emergency Notification.

To input emergency contacts: create a node of type "Emergency Contacts" and fill out
your primary and secondary emergency contacts.  Note if you create more than one node
of this type the RSS feed will only show the most recently updated, you will probably
not want to create more than one node of this type, but instead just update one single node
with the most up-to-date contact information.


