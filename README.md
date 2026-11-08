# Evaluation

## Firebase setup

The site uses Firebase Authentication and Cloud Firestore for account sign-in and live schedule sync.

1. In Firebase Authentication, enable Google and Email/Password sign-in. Add `eva.sni.org.in` to the authorized domains.
2. Verify the admin email account `admin11008@gmail.com` has Auth UID `6NguI1ON0Dg95qeJNeXnbw2aRyX2`. The admin login ID is `surya11008`; Firebase verifies the password.
3. In Cloud Firestore, open **Rules**, replace the current rules with [`firestore.rules`](./firestore.rules), and publish. Until these rules are published, the site does not have server-enforced member/admin access.
4. Open the site and sign in. The admin can use **Import** to load `schedule_data.json`; schedules and subjects then sync live through Firestore.

With these rules, any Google account that signs in can read schedules. Email/Password users must exist in Firebase Authentication. For access limited to an approved member list, add a member-UID allowlist to the rules before publishing them.