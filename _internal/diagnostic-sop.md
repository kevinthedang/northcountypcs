# Diagnostic SOP (internal)

Not published to the website. The home page deliberately shows only the **deliverables** of a
diagnostic, not this procedure — publishing a numbered method turns it into a checklist a
customer can audit you against if a repaired fault comes back.

> **Visibility:** this lives in `_internal/`, which Jekyll-based GitHub Pages ignores, so it
> is not served at northcountypcs.com. If you ever switch to an Actions deploy that uploads
> the whole repo, move this file out of the repository first.

## Timing

| Tier | Time | Price |
| --- | --- | --- |
| Quick check | ~15 min | Free |
| Full diagnostic | 60–90 min on the bench | $49 |

**These are internal targets, not published commitments.** The website deliberately shows no
durations — a stated time becomes a promise a customer can hold you to on a machine that turns
out to need longer. Pace yourself against them, don't advertise them.

If a full diagnostic runs well past ~90 minutes, check in with the customer before continuing.

## Steps

1. **Intake.** Record what is wrong and how it happened. When was the system built, how often
   is it used, and what is it used for — gaming, productivity, or casual use?
2. **Reproduce the issue.** Observe it directly. If it can't be reproduced, say so in the
   findings rather than guessing.
3. **Physical and startup checks.** Inspect the case, fans and their orientation, cable
   connections. Check BIOS.
4. **Hardware health.** GPU and CPU temperatures, memory tests, SMART storage tests.
5. **Software health.** Review system errors, drivers, updates, and configuration issues.
6. **Targeted testing.** Controlled tests that reproduce crashing, overheating, or performance
   issues. **Stop if trouble smells** — define that as: any test that risks data loss, risks
   damage to the hardware, or pushes past the 90-minute ceiling. Call the customer first.
7. **Write down findings.** Give the client: symptoms reproduced, tests performed, likely
   cause, recommended fixes with estimated parts and labor, and anything you could not verify.

## Deliverable

Every full diagnostic ends with written findings. Minimum content:

- Symptoms reproduced (or explicitly: not reproduced)
- Tests performed and their results
- Likely cause
- Recommended fix, with parts and labor estimated separately
- Anything unverified, and why

## Gaps to decide before the site goes live

- [x] ~~Is the $49 credited toward the repair if the customer accepts the quote?~~ **Decided:
      yes.** Credited, not refunded. Quoted on the site as "The $49 comes off the repair if you
      go ahead." Declining the quote still costs $49.
- [ ] Should the credit apply to *all* repairs, or only above a threshold (e.g. $100)? At a
      $49 credit on an $80 repair you're working nearly for free.
- [ ] If a repair costs less than $49, is the difference eaten or does the customer pay the
      diagnostic in full?
- [ ] Do you image or back up a drive before running destructive tests? If not, add a line to
      the intake form that the customer is responsible for their own backups.
- [ ] How long do you hold a machine after the customer declines the quote?
- [ ] Is there a warranty on labor, on parts, or neither?
- [ ] At 60–90 minutes of bench time, $49 works out to roughly $33–49/hour before parts. Either
      cap it at 60 minutes, credit it toward the repair, or raise the fee.
