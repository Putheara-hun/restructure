# Restructure Loan — module prototype

A working mock of the KOMCHEY LMS **Restructure Loan** screen, for review and sign-off before
the build is finished.

Open **[index.html](index.html)** — or the GitHub Pages link for this repository — in any browser.
One self-contained file, no install, no server, no internet needed once loaded.

## What it does

Pick a customer, set the restructure method, type a figure, and the schedule and the printable
report rebuild live. The calculation is a direct port of `LN.FV_SCHEDULE_RESTRUCTURE`, so any
tenor or ability amount can be tried, not only the prepared examples.

| Method | What the officer enters | What the system works out |
| --- | --- | --- |
| Extend Number of Tenor | instalments to add | new tenor = remaining + added |
| Ability to Repayment | amount per instalment | how many instalments clear the debt |
| Customer Schedule | the schedule by hand | nothing — manual entry |

**Remaining Tenor** fills in from the customer selection alone, and re-counts if the Transaction
Date changes. It counts instalments **not yet due**; overdue ones are listed separately in red, so
the figure can be read straight off the grid. Past the maturity date it is zero.

The schedule is colour-banded: grey settled history, red overdue, blue the new schedule on dates
the loan already had, green the dates the restructure added.

## Demonstration accounts

| Customer | Frequency | Situation |
| --- | --- | --- |
| SOK Dara | Daily | 20 of 30 paid — remaining tenor 10 |
| CHAN Sreypov | Daily | past maturity — remaining tenor 0, 8 overdue |
| LIM Sokhan | Monthly | 40,000 outstanding — the ability-to-repay case |
| VANN Rithy | Monthly | part paid, part overdue, part still to fall due |
| PHAL Doungchan | Weekly | shows what "tenor" means on a non-daily loan |

## Please read before testing

- **The data is invented.** These five accounts do not exist. Names, CIF numbers and contract
  numbers were made up so the arithmetic can be checked by hand. No customer record was used.
- **Nothing is saved.** Save shows a message and writes nothing — there is no database behind it.
- **Fees and holiday skipping are simplified** so the tenor arithmetic is the only thing to verify.
  Both work normally in the real module.

## Points still to agree

These come up as warnings in the prototype at the moment they occur:

1. **Overdue instalments** are closed off at the restructure date — unpaid principal moves into the
   new schedule, unpaid interest and fees are written off. Confirm this is intended.
2. **Ability to Repayment can shorten a loan** when the stated ability is higher than the current
   instalment. Allow it, warn, or block?
3. **A very small final instalment** can appear (e.g. 13.44). Fold it into the instalment before it?
4. **"Tenor" means instalments, not days.** On a weekly or monthly loan, 20 is 20 instalments.
5. **The printed report** shows old and new together. The original specification asked for the new
   schedule only, starting at the restructure date.
