# Evaluation

## Firebase setup

The site uses Firebase Authentication and Cloud Firestore for account sign-in and live schedule sync.

1. In Firebase Authentication, enable Google and Email/Password sign-in. Add `eva.sni.org.in` to the authorized domains.
2. Verify the admin email account `admin11008@gmail.com` has Auth UID `6NguI1ON0Dg95qeJNeXnbw2aRyX2`. The admin login ID is `surya11008`; Firebase verifies the password.
3. In Cloud Firestore, open **Rules**, replace the current rules with [`firestore.rules`](./firestore.rules), and publish. Republish these rules whenever this file changes; category management and shared column ordering require the `categories` and `tableSettings` rules. Until the rules are published, the site does not have server-enforced member/admin access.
4. Open the site and sign in. The admin can use **Import** to load `schedule_data.json`; schedules and subjects then sync live through Firestore.

With these rules, any Google account that signs in can read schedules. Email/Password users must exist in Firebase Authentication. For access limited to an approved member list, add a member-UID allowlist to the rules before publishing them.

## Schedule features

- The default date range is the current Sunday–Saturday week. Use the week arrows or the name, subject, and date filters to find schedules.
- Admins can check off each subject. All signed-in users can see its completion checkbox and completion timestamp; only the admin can change it.
- Admins can postpone one subject to a later date or move the whole schedule (and all its subjects) to a later date range. Changes sync through Firestore.
- Schedule records show each person's completion percentage across all their subjects. The **Status & Rankings** tab sorts the filtered people by percentage and shows completed subjects and timestamps.
- Admins assign each person a Position: Overseer, (D)Overseer, Deacon, BCL, PBCL, Group Leader, Unit Leader, Co-Worker, Evangelist, Member, or Other. The Position filter applies to both Schedule and Status & Rankings.
- Each subject has a consistent, distinct color. Admins can assign Type 1 through Type 10 to each schedule; Type appears beside Position and can filter both Schedule and Status & Rankings.
- Admins can add or rename Position and Type options in the schedule form. Renaming an option updates all schedules assigned to it.
- The shared filters (name, subject, Position, Type, and week/date range) apply to both Schedule and Status & Rankings.
- Admins can use the left/right arrows in either table header to reorder columns. The order syncs to all signed-in users through Firestore and requires publishing the `tableSettings` rule in [`firestore.rules`](./firestore.rules).
- Telugu text uses the Sree Krushnadevaraya font when the Google Fonts stylesheet is available.
- Admins can duplicate a schedule from its row/card actions. The copy starts with “(Copy)” in its name, retains its Position, dates, subjects, and postponed dates, and resets completion progress.