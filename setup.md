# Setup

## 1. Choose storage

Create a task ledger, a decision ledger, and a small state record containing:

- the current Monday-starting week;
- whether a thirst signal has been posted for that week; and
- the last successful hourly check time.

JSON, CSV, a database, or a spreadsheet can work.

## 2. Set the timezone

Choose the timezone used for Monday resets and weekly boundaries. Use that timezone consistently for decisions, pace calculations, and scheduled checks.

## 3. Configure the hourly job

Schedule the checker at the top of every hour. It should:

1. load the current week;
2. count only explicit awards minus explicit revocations;
3. compare the total with the path to 10;
4. remain silent when on pace;
5. post a signal only when behind and no signal has already been sent that week; and
6. save the updated state atomically.

## 4. Configure the destination

Give the checker permission to post in `#general`. Do not embed personal details, credentials, private channel identifiers, or private task data in the code or message.

Suggested signal:

> I’m behind pace for 10 cookies this week. Send me one concrete project I can finish to earn one.

## 5. Test safely

Run a dry test with temporary state and verify:

- an on-pace result produces no message;
- an at-risk result produces the short signal;
- a second run does not repeat the signal;
- a Monday rollover opens a new week;
- a task completion does not create an award; and
- only an explicit reviewer decision changes the cookie total.

## 6. Operate

Review the ledger on Monday, preserve prior weeks, and investigate any missed hourly runs. Keep the automation deterministic and the award authority human.
