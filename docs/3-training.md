---
icon: lucide/book-open-check
---

# 3. Trainings

Once a user learns about equipment on the MakeACS website, we should put their knowledge to the test! MakeACS has an integrated training system, that ties into the [access control system](./4-access-control.md), to lock equipment usage behind trainings and sign-offs. 

## Training Configuration

Managers can assign training requirements to a specific piece of equipment, or to an entire room (such that it is required by all equipment in that room). Trainings can be *reciprocal*, for instance finishing the "Drill Press Safety" training for a drill press in the wood shop can also count for a drill press in the metal shop. 

Edits to trainings go out immediately, and do not necessarily invalidate previous passes of a training. Trainings can also be archived to temporarily hide them, and remove them from all equipment.

Managers can also set a training's expiration policy. Trainings can be configured to require a regular re-completion to maintain access, or a training can be good forever once passed. When a training is nearing expiration, users will get an email reminding them to renew it.

![Image](./assets/training%20expiration%20notice.png)

Users can see training requirements for each piece of equipment via a "Training Checklist" on the website. If a training has an expiration date, the expiration can be checked here as well.

The MakeACS website also serves a mobile-friendly version of the training checklist, designed to be accessed via QR code at the machine in case a user finds they do not have access. This page will also diagnose other access restriction issues, such as a user having a [hold](./5-shop-management.md#user-restrictions) on their account.

![Image](./assets/training%20checklist.jpg)

## Online Trainings

The primary form of trainings associated with MakeACS are online trainings. These can be taken at any time by users, and support both desktop and mobile-friendly formatting. 

Trainings can be comprised of (markdown) text, images, videos, PDFs, and multiple-choice single-answer or multi-answer questions. Trainings are created and edited via a simple training editor baked into the MakeACS website, accessible to managers. 

![Image](./assets/quiz%20content.png)
/// caption
An example of an embedded video training, pulled from YouTube
///

Managers can configure the required pass rate for an online training to be considered complete. To help users score better, questions can be configured with a hint and affirmation, given to the user as feedback when they complete a training. 

![Image](./assets/training%20feedback.png)

To prevent brute-force completions, a user who fails a training 3 times in a day has that specific training locked for 24 hours. This is recorded for [audit](./6-statistics-logging.md) purposes, and can be overridden by staff if needed. 

!!! info
    The completion of a training can also be used to trigger an API call - for instance at RIT, completing the training on how to use 3DPrinterOS grants your 3DPrinterOS account access to submit prints!

## In-Person Checks

The second form of trainings associated with MakeACS are in-person checks. These require a user to come in-person, and work with a trainer to demonstrate competency, review the function of the equipment, etc. 

In-person checks can be configured to be completable by any staff within the equipment's space, or by a select list of designated trainers. 

!!! tip
    Staff cannot perform an in-person check on equipment they themselves do not have the check completed on. Furthermore, staff are blocked from signing off their own account's in-person checks.

In-person checks are not available for sign-off until the user has completed any relevant online trainings. 

To help users prepare for (and to remind staff of what topics to cover in) an in-person check, each piece of equipment can optionally have a link set with information on the in-person check. This link would be found in the training checklist, along with online trainings.