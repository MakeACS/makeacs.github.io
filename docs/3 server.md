---
icon: lucide/globe-code
---

# 3. Server Features

The server (aka the website) is how all makers and staff interact with MakeACS, as well as the central source of information for the MakeACS hardware.

The website is designed to require minimal resources to host, with hosting from most providers working out to under $30 per month. It can also easily be deployed in a docker container for hosting in on-campus IT infrastructure, to both save costs and comply with institutional data handling policies. 

The website implements Shibboleth SAML Single Sign On, to easily integrate into existing systems. Local accounts are possible for institutions that do not have SSO, or for special non-SSO cases, like organization accounts.

## Public Information

The website hosts a public-facing website for the shops, with useful information for the general public;

* Facility hours, with support for special-case hours and differing hours for different rooms.
* Announcements with an integrated call-to-action link.
* Facility information such as locations, links to maps, etc.
* General machine information.
* Real-time equipment availability, to see if what you are looking to use is free.
* A publicly-available REST API for getting the hours, announcements, etc. for integration into other systems and websites.

Additionally, the website generates and serves pages for the hours and announcements that can be constantly displayed on screens around the facility, that will automatically update as changes are made to the website, and handle anti-burn in image shifting.

## Maker (User) Features

Once a maker signs in, they can access more features of the website;

### SSO Information Sync

TOn log-in the system can get a user's preferred name, preferred pronouns, and profile picture. This information can then be readily accessed by staff, to ensure they are properly addressing users as they work in the shop. If a user's preferred pronouns are not yet updated at the SSO-level, they can be manually changed within their user preferences.

The system can also be configured to restrict a user account based on SSO information. For instance, at RIT alumni maintain their normal SSO account, but are no longer allowed to use the makerspaces. So, when an alumni logs into the website, their account is flagged and put into an archived state, where they can no longer use equipment. 

Analytical data can also be collected via SSO and plotted against other data gathered about shop operation, such as correlating equipment usage trends to home college, or makerspace utilization vs. expected graduation year.

### Trainings

One of the main features used by makers on the website is the training system. Online trainings are a great way to reinforce general safety and usage concepts before users step foot in the shop. Trainings consist of multiple-choice questions supporting either single-answer or multiple-answer results. The training system also supports embedding images, PDFs, videos, and markdown-formatted text directly inside the training. 

Shop administrators can set pass and refresh policies for trainings. For instance, RIT requires an 80% or higher to have considered "passing" a training, and makes any training related to safety expire annually, whereas technical trainings last forever. 

To prevent brute-forcing, the website automatically locks out a user for 24 hours if they attempt and fail a training 3 times in a day. This is logged for auditing, and can be overridden by staff if needed.

Training content can be reciprocal across any equipment within the same MakeACS server. For example, at RIT there is a generic "How to use the MakeACS card reader" training that is required before using any equipment. Once the user completes it in the machine shop, it is reciprocally granted in the sewing shop, for example. 

Training content can be associated with equipment, rooms, or the entire makerspace to ensure consistent application of policies. 

As a training approaches expiration, makers are automatically sent reminder emails, with a call to action on what trainings to complete to continue having access to which equipment(s).

To help inform users about training requirements, every piece of equipment on the website has a checklist and a progress bar. The website also generates mobile-friendly training checklists, intended for use with a QR code on the machine.

### Reservations

While the default behavior of equipment in MakeACS is first-come, first-serve, the system also implements a reservation calendar. Equipment can be configured to have a self-schedule calendar where anyone can put a reservation down, or staff-schedule, where users muse work with staff to schedule an appointment. Appointment scheduling can optionally be blocked behind the same training access checks that machine access would, so users cannot reserve equipment they cannot use.

## Staff Features

System administrators can designate two tiers of staff within MakeACS; staff, and managers. These roles can be assigned on a per-space basis, so staff only have elevated permissions in areas they work in. With a staff account, more features become available;

### Staff Sign-Off

Trainings can be just one part of granting access to equipment; the system can be configured to also (or instead of trainings) require an in-person staff sign-off on a per-machine basis. These trainings can have a configurable expiration policy, and can be set to either be permitted by any staff, or a select list of authorized trainers. 

Staff Sign-Offs are visible to other staff as a way of verifying training completion, or if needed a way to revoke equipment access, and a record is kept of which staff completed a user's training. 

### Audit Logs

All activities in the facility is tracked in a centralized audit log/history. Log information can be sorted and searched by keywords, category, or date range. System administrators can set certain information to not be visible to all staff, such as training grades. 

The audit log embeds useful click-through links. For example, the audit log of "Jim Heaney has signed into the Atrium Makerspace" has a click-through to Jim Heaney's user account, so staff can quickly access information on them. 

### Maintenance Logs

To aid in tracking equipment issues, a maintenance logging system is available to all staff. Staff can open reports with issues they find, and attach images to assist in future diagnostics. Which staff claim/close a ticket, how long the ticket took to close, and how often tickets of a set severity level are registered against a piece of equipment are all logged for statistical analysis. 

In addition to reported issues, the MakeACS server can automatically generate tickets, based on 2 different criteria;

* Time-based tickets are opened a set interval after their last iteration were closed. An example is a weekly reminder to check the eye wash stations.

* Usage-based tickets are opened after a set amount of on-time from the MakeACS hardware. An example is a ticket to change the oil on the waterjet every 50 hours.

Maintenance logs that are marked with a high severity can be configured to automatically lock out equipment and deny all access attempts.

### Equipment State

Staff have the ability to see the equipment's current state, and remotely change the equipment's state via the website. This allows them to lock equipment on during workshops or trainings, or lock it off when the equipment should not be used. Staff are only able to lock equipment on that they themselves are trained on, to prevent system bypasses. If staff forget to return equipment from the locked-on to regular mode, systems re-lock automatically at 4am every morning. Locked out equipment will maintain its state, even through a loss-of-power. 

Staff can see the current equipment state, and either the current user or what staff commanded it into that state via the website. 

### Inventory Control

The MakeACS server supports a full inventory management system, that either be accessed via API or via manual staff action. Staff can add or remove inventory via the normal MakeACS website, or via special mobile-optimized pages that are intended to be on QR codes directly attached to the inventory. 

Managers can set categories, price points, and restock policies for all inventory. When inventory goes below a set threshold, the system can automatically send a Slack or email notification to trigger a re-order.

Inventory items can have images or notes attached to them, to help staff identify them or to have re-order information on hand in one centralized location. 

### Tool Loan Tracking

For high-value or high-risk equipment, the website has a tool loan tracking system. Users can check out equipment with a staff member, and return it when complete. If a user forgets to return equipment for more than 24 hours, a flag is put up to follow up with the user.

Upon loaning or returning equipment, staff can be presented with images and/or formatted text, to verify they are giving the correct item and everything is as it should be. Staff can note damage or issues upon return for investigation.

The condition and current loan status of all equipment can be seen from a centralized interface, and is also available for statistical analysis via the audit log.

### User Restrictions

In the event that staff find a user acting in an improper or dangerous way in the makerspace, they have the ability to place a restriction on their account. This will flag their account for review by a manager, and stop them from using any equipment in the makerspace until it is resolved.

Managers have the ability to place a hold on a user's account, which stops them from using all equipment under MakeACS, notifies staff if they attempt to sign in to a makerspace, and locks down their view of the website. Even when removed, a permanent record of a hold is left on the user's account. 

Staff and managers can also see and edit notes on a user's account, to help log information for other staff.

### Organizations & Finances

Managers have the ability to credit user accounts with a virtual currency - Construct Credits - that can be used to purchase items from inventory, or as part of automated payment integrations with systems like 3DPrinterOS, in addition to PaperCut.

In addition to being able to issue such credits to individual users, managers can create organization accounts and issue credits to them. This allows research labs, student teams, and more to operate under one financial umbrella, rather than having to designate a single point-of-contact. 