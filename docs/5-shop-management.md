---
icon: lucide/package-search
---

# 5. Shop Management

To make operations smoother, MakeACS integrates a number of shop management tools, available only to staff and managers.

!!! note
    Managers are an elevated permission level, anything that is noted as something a staff can do, a manager can do as well.

## Tool Loaning

For high-value, high-risk, or in high-demand resources that would not be suitable for a traditional [reservation calendar](./2-website.md#reservations), the website implements a loan-out tracking system. Users can check out equipment with a staff member, and return it when complete. If a user forgets to return equipment for more than 24 hours, a flag is raised to follow up with the user.

Upon loaning or returning equipment, staff can be presented with images and/or formatted text, to verify they are giving the correct item and everything is as it should be. Staff can note damage or issues upon return for investigation. Current loan or damage states, and historical usage data, can all be used in [statistical analysis](./6-statistics-logging.md).

![Image](./assets/make%20tool%20loan.png)

## History

To help staff better understand what is happening in the shop, a real-time history page is visible. This shows every action taken within the space in chronological order, with the ability to search and filter it.

The history embeds useful click-through links, to help staff more efficiently complete their jobs. For example, the audit log "Jim Heaney has signed into the Atrium Makerspace" has a click-through to Jim Heaney's user account, so staff can quickly access information on them. 

This data can be used to draw [statistical conclusions](./6-statistics-logging.md) on shop operations as well.

![Image](./assets/make%20history.png)
///caption
Names of actual users redacted from screenshot
///

## Equipment State

Staff have the ability to see the real-time state of all equipment in the space, including the current user if in-use. Staff also have the ability to remotely set the state of the equipment to either lock it out, such as in the event of needing maintenance, or locking it always on, such as for a workshop or training. Staff only have the ability to lock on equipment while in the space (enforced by physical sign-in), and only for equipment they themselves are trained on. 

!!! note
    If a staff forgets to reset an always-on machine, it is automatically returned to the idle state every morning at 4am. Equipment in the locked-out state remains that way, even through a power cycle, until lifted by a staff.

![Image](./assets/machine%20states.png)
///caption
This view also Hobbs time, see [statisitics](./6-statistics-logging.md) for more info.
///

## Inventory Control

The MakeACS server has an integrated inventory management system, for tracking consumables, spare parts, and for-sale items. Staff can add or remove inventory via the normal MakeACS website, or via special mobile-optimized pages that are intended to be on QR codes directly attached to the inventory. Inventory can also be managed through an API, to enable more complex integrations.

Managers can set categories, price points, and restock policies on a per-item level. When inventory goes below a set threshold, the system can automatically send a Slack or email notification to trigger a re-order.

Inventory items can have images or notes attached to them, to help staff identify them or to have re-order information on hand in one centralized location. 

![Image](./assets/make%20slackbot%20inventory.png)
///caption
Time to order more filament!
///

## Maintenance Logs

To aid in tracking equipment issues, a maintenance logging system is available to all staff. Staff can open reports with issues they find, and attach images to assist in future diagnostics. Which staff claim/close a ticket, how long the ticket took to close, and how often tickets of a set severity level are registered against a piece of equipment are all logged for statistical analysis. 

!!! tip
    The [At-Machine Training QR Codes](./3-training.md#training-configuration), when scanned by a staff, provide a mobile-friendly maintenance report page! This makes it easy to report issues when staff spot them, rather than having to go to a computer.

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

## User Restrictions

In the event that staff find a user acting in an improper or dangerous way in the makerspace, they have the ability to place a restriction on their account. This will flag their account for review by a manager, and stop them from using any equipment in the makerspace until it is resolved.

Managers have the ability to place a hold on a user's account, which stops them from using all equipment under MakeACS, notifies staff if they attempt to sign in to a makerspace, and locks down their view of the website. Even when removed, a permanent record of a hold is left on the user's account. 

Staff and managers can also see and edit notes on a user's account, to help log information for other staff.

![Image](./assets/make%20hold.png)


## Organizations & Finances

Managers have the ability to credit user accounts with a virtual currency - Construct Credits - that can be used to purchase items from inventory, or as part of automated payment integrations with systems like 3DPrinterOS, supplementing funds from traditional sources like PaperCut or Atrium.

In addition to being able to issue such credits to individual users, managers can create organization accounts and issue credits to them. This allows research labs, student teams, etc. to operate under one financial umbrella, rather than having to designate a single point-of-contact. 