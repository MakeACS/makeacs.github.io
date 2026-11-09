---
icon: lucide/globe-code
---

# 3. Server Features

The server (aka the website) is how all makers and staff interact with MakeACS, as well as the central source of information for the MakeACS hardware.

The website is designed to require minimal resources to host, with hosting from most providers working out to under $30 per month. It can also easily be deployed in a docker container for hosting in on-campus IT infrastructure, to both save costs and comply with institutional data handling policies. 

The website implements Shibboleth SAML Single Sign On, to easily integrate into existing systems. Local accounts are possible for institutions that do not have SSO, or for special non-SSO cases, like organization accounts.

The website's appearance is fully customizable through a zero-code graphical interface, and supports multiple appearance skins that users can select from (such as a dark or light mode, seasonal themes, etc.).

![Image](./assets/make%20homepage.png)
///caption
The MakeACS homepage at the RIT SHED Makerspaces
///

## Public Information

The website hosts a public-facing website for the shops, with useful information for the general public;

* Facility hours, with support for special-case hours and differing hours for different rooms.
* Announcements with an integrated call-to-action link.
* Facility information such as locations, links to maps, etc.
* General machine information.
* Real-time equipment availability, to see if what you are looking to use is free.
* A publicly-available REST API for getting the hours, announcements, etc. for integration into other systems and websites.
* Upcoming events, pulled via API from systems like Eventbrite.

Additionally, the website generates and serves pages for the hours, announcements, and events that can be constantly displayed on screens around the facility. These screens will automatically update as changes are made to the website, and handle anti-burn in image shifting. They are designed to be extremely easy to display, so a cheap Raspberry Pi Zero connected to the back of the TV can handle it.

![Image](./assets/make%20hours%20display.png)
/// caption
Check it out yourself; [make.rit.edu/app/display/hours/36](https://make.rit.edu/app/display/hours/36)
///

![Image](./assets/make%20displays.jpg)
/// caption
Upcoming Events, Hours, and Announcements Displays
///

## Maker (User) Features

Once a maker signs in, they can access more features of the website;

### SSO Information Sync

On log-in the system can get a user's preferred name, preferred pronouns, and profile picture. This information can then be readily accessed by staff, to identify a user and ensure they are properly addressing them. If a user's preferred pronouns are not yet updated at the SSO-level, they can be manually changed within their user preferences.

The system can also be configured to restrict a user account based on SSO information. For instance, at RIT alumni maintain their normal SSO account, but are no longer allowed to use the makerspaces. So, when an alumni logs into the website, their account is flagged and put into an archived state, where they can no longer use equipment. 

Analytical data can also be collected via SSO and plotted against other data gathered about shop operation, such as correlating equipment usage trends to home college, or makerspace utilization versus expected graduation year.

![Image](./assets/make%20user%20info.png)
/// caption
User info visible to staff, pulled from SSO
///

### Trainings

One of the main features used by makers on the website is the training system. Online trainings are a great way to reinforce general safety and usage concepts before users step foot in the shop. Trainings consist of multiple-choice questions supporting either single-answer or multiple-answer inputs. The training system also supports embedding images, PDFs, videos, and markdown-formatted text directly inside the training. 

![Image](./assets/quiz%20content.png)
/// caption
An example of an embedded video training
///

When a user completes a training, they can be given customized affirmations and/or hints to either reinforce concepts, or give them a nudge towards the correct answer.

![Image](./assets/training%20feedback.png)

Shop administrators can set pass and refresh policies for trainings. For instance, RIT requires an 80% or higher to have considered "passing" a training, and makes any training related to safety expire annually, whereas technical trainings last forever once completed. 

To prevent brute-forcing, the website automatically locks out a user for 24 hours if they attempt and fail the same training 3 times in a day. This is logged for auditing, and can be overridden by staff if needed.

Training content can be reciprocal across any equipment within the same MakeACS server. For example, at RIT there is a generic "How to use the MakeACS card reader" training that is required before using any equipment. If the user completes it to use a drill press, they'll also have it complete when they go to look at sewing machine requirements in another shop.

Training content can be associated with equipment, rooms, or the entire makerspace to ensure consistent application of policies. 

As a training approaches expiration, makers are automatically sent reminder emails, with a call to action on what trainings to complete to continue having access to which equipment(s).

![Image](./assets/training%20expiration%20notice.png)
///caption
I'll lose access to the 3D printers if I don't re-do my training!
///

To help inform users about training requirements, every piece of equipment on the website has a checklist and a progress bar. The website also generates mobile-friendly training checklists, intended for use with a QR code on the machine. Scanning this QR code also gives users an automated troubleshooter to diagnose why they were unable to access a piece of equipment.

![Image](./assets/training%20checklist.jpg)
///caption
Users can see what trainings are needed, and when the completed ones expire.
///

### Reservations

While the default behavior of equipment in MakeACS is first-come, first-serve, the system also implements a reservation calendar. Equipment can be configured to have a self-schedule calendar where anyone can put a reservation down, or staff-schedule, where users must speak with staff to schedule an appointment. In both cases, the calendar is publicly visible with redacted user information, so other users known when equipment is usable. Appointment scheduling can optionally be blocked behind the same training access checks that machine access would, so users cannot reserve equipment they cannot use.

When a reservation is submitted, staff with authority to approve it can be notified by email or Slack message.

![Image](./assets/make%20slackbot%20reservation.png)

![Image](./assets/make%20reservation.png)
///caption
The self-serve reservation calendar
///

## Staff Features

System administrators can designate two tiers of staff within MakeACS; staff, and managers. These roles can be assigned on a per-space basis, so staff only have elevated permissions in areas they work in. With a staff account, more features become available;

### Staff Sign-Off

Trainings can be just one part of granting access to equipment; the system can be configured to also (or instead of trainings) require an in-person staff sign-off on a per-machine basis. These trainings can have a configurable expiration policy, and can be set to either be completable by any staff, or a select list of authorized trainers. 

### Audit Logs

All activities in the facility are tracked in a centralized audit log/history. Log information can be sorted and searched by keywords, category, and/or date range. Some sensitive information is only visible to managers, such as training grades.

The audit log embeds useful click-through links, to help staff more efficiently complete their jobs. For example, the audit log "Jim Heaney has signed into the Atrium Makerspace" has a click-through to Jim Heaney's user account, so staff can quickly access information on them. 

![Image](./assets/make%20history.png)
///caption
Names of actual users redacted from screenshot
///

Audit log content can also be fed into systems like Grafana to develop graphical data representations, identify trends, or have real-time heads-up information about the shop. For example, the visualization below allows tracking of sign-ins to a room per hour, to identify when additional staffing is needed.

![Image](./assets/users%20by%20hour.png)

For further analytics collection specifically surrounding the website, you can enter a custom Google Analytics ID to gain usage information, such as common pages, traffic sources, and bounce rates.

### Maintenance Logs

To aid in tracking equipment issues, a maintenance logging system is available to all staff. Staff can open reports with issues they find, and attach images to assist in future diagnostics. Which staff claim/close a ticket, how long the ticket took to close, and how often tickets of a set severity level are registered against a piece of equipment are all logged for statistical analysis. 

!!! tip
    Remember the QR codes for users to scan at a machine, so they can see training progress? If staff scan them, they are brought instead to a mobile-friendly maintenance ticket page to report issues in-situ.

When a maintenance ticket is generated, it can be used to trigger an automatic email or Slack message, to keep maintenance staff informed about ongoing issues.

![Image](./assets/make%20slackbot%20maintenance.png)
///caption 

///

In addition to reported issues, the MakeACS server can automatically generate tickets, based on two different criteria;

* Time-based tickets are opened a set interval after their last iteration was closed. An example is a weekly reminder to check the eye wash stations.

* Usage-based tickets are opened after a set amount of on-time from the MakeACS hardware. An example is a ticket to change the oil on the waterjet every 50 hours.

Maintenance logs that are marked with a high severity can be configured to automatically lock out equipment and deny all access attempts.

![Image](./assets/make%20maintenance.png)
///caption
"SERVER" tickets are for scheduled/regular maintenance
///

The Hobbs Timer, or total on-time timer, can be reset per-equipment by managers to assist in tracking usage over a major time span. This is independent of the audit log, so cumulative usage can still be monitored in addition to using this as a "trip odometer". You can see the Hobbs Timers for sewing machines in the screenshot below, in *Equipment State*.

### Equipment State

Staff have the ability to see the equipment's current state, and remotely change the equipment's state via the website. This allows them to lock equipment on during workshops or trainings, or lock it off when the equipment should not be used. Staff are only able to lock equipment on that they themselves are trained on, to prevent system bypasses. If staff forget to return equipment from the locked-on to regular mode, systems reset at 4am every morning. Locked out equipment will maintain its state, even through a loss-of-power, until commanded out of it by a staff member.

![Image](./assets/machine%20states.png)
///caption
If equipment is in use, staff can see the current user's name
///

### Inventory Control

The MakeACS server has an integrated inventory management system, for tracking consumables, spare parts, and for-sale items. Staff can add or remove inventory via the normal MakeACS website, or via special mobile-optimized pages that are intended to be on QR codes directly attached to the inventory. Inventory can also be managed through an API, to enable more complex integrations.

Managers can set categories, price points, and restock policies on a per-item level. When inventory goes below a set threshold, the system can automatically send a Slack or email notification to trigger a re-order.

Inventory items can have images or notes attached to them, to help staff identify them or to have re-order information on hand in one centralized location. 

![Image](./assets/make%20slackbot%20inventory.png)
///caption
Time to order more filament!
///

### Tool Loan Tracking

For high-value or high-risk tools and equipment, the website has a tool loan tracking system. Users can check out equipment with a staff member, and return it when complete. If a user forgets to return equipment for more than 24 hours, a flag is put up to follow up with the user.

Upon loaning or returning equipment, staff can be presented with images and/or formatted text, to verify they are giving the correct item and everything is as it should be. Staff can note damage or issues upon return for investigation.

The condition and current loan status of all equipment can be seen from a centralized interface, and is also available for statistical analysis via the audit log.

![Image](./assets/make%20tool%20loan.png)

### User Restrictions

In the event that staff find a user acting in an improper or dangerous way in the makerspace, they have the ability to place a restriction on their account. This will flag their account for review by a manager, and stop them from using any equipment in the makerspace until it is resolved.

Managers have the ability to place a hold on a user's account, which stops them from using all equipment under MakeACS, notifies staff if they attempt to sign in to a makerspace, and locks down their view of the website. Even when removed, a permanent record of a hold is left on the user's account. 

Staff and managers can also see and edit notes on a user's account, to help log information for other staff.

![Image](./assets/make%20hold.png)

### Organizations & Finances

Managers have the ability to credit user accounts with a virtual currency - Construct Credits - that can be used to purchase items from inventory, or as part of automated payment integrations with systems like 3DPrinterOS, in addition to PaperCut.

In addition to being able to issue such credits to individual users, managers can create organization accounts and issue credits to them. This allows research labs, student teams, etc. to operate under one financial umbrella, rather than having to designate a single point-of-contact. 